---
title: "Azure CLI 스크립트 샘플 - App Service 계획에서 함수 앱 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - App Service 계획에서 함수 앱 만들기"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 40c3fa6fa6c07d59e4bf55531e116ba50aa92b91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="67ee7-103">App Service 계획에서 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="67ee7-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="67ee7-104">이 샘플 스크립트는 함수에 대한 컨테이너인 Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="67ee7-105">함수 앱은 전용 App Service 계획을 사용하여 생성됩니다. 이는 서버 리소스가 항상 켜져 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-105">The Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="67ee7-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="67ee7-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="67ee7-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67ee7-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="67ee7-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="67ee7-109">Sample script</span></span>

<span data-ttu-id="67ee7-110">이 스크립트는 전용 [App Service 계획](../functions-scale.md#app-service-plan)을 사용하는 Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

<span data-ttu-id="67ee7-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "App Service 계획에서 Azure Function 만들기")]</span><span class="sxs-lookup"><span data-stu-id="67ee7-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="67ee7-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="67ee7-112">Script explanation</span></span>

<span data-ttu-id="67ee7-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="67ee7-114">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-114">This script uses the following commands:</span></span>

| <span data-ttu-id="67ee7-115">명령</span><span class="sxs-lookup"><span data-stu-id="67ee7-115">Command</span></span> | <span data-ttu-id="67ee7-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="67ee7-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="67ee7-117">az group create</span><span class="sxs-lookup"><span data-stu-id="67ee7-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="67ee7-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="67ee7-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="67ee7-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="67ee7-120">Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="67ee7-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="67ee7-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="67ee7-122">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="67ee7-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="67ee7-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="67ee7-124">Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-124">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="67ee7-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67ee7-125">Next steps</span></span>

<span data-ttu-id="67ee7-126">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67ee7-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="67ee7-127">추가 Azure Functions CLI 스크립트 샘플은 [Azure Functions 설명서](../functions-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67ee7-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
