---
title: "CLI 스크립트 샘플-aaaAzure 앱 서비스 계획에서 함수 응용 프로그램 만들기 | Microsoft Docs"
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
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="075c5-103">App Service 계획에서 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="075c5-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="075c5-104">이 샘플 스크립트는 함수에 대한 컨테이너인 Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="075c5-105">hello 함수 응용 프로그램을 통해 서버 리소스에는 항상 의미 전용된 앱 서비스 계획을 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="075c5-106">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="075c5-107">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="075c5-108">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="075c5-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="075c5-109">Sample script</span></span>

<span data-ttu-id="075c5-110">이 스크립트는 전용 [App Service 계획](../functions-scale.md#app-service-plan)을 사용하는 Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="075c5-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="075c5-111">Script explanation</span></span>

<span data-ttu-id="075c5-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="075c5-113">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="075c5-114">명령</span><span class="sxs-lookup"><span data-stu-id="075c5-114">Command</span></span> | <span data-ttu-id="075c5-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="075c5-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="075c5-116">az group create</span><span class="sxs-lookup"><span data-stu-id="075c5-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="075c5-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="075c5-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="075c5-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="075c5-119">Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="075c5-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="075c5-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="075c5-121">App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="075c5-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="075c5-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="075c5-123">Azure 함수 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="075c5-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="075c5-124">Next steps</span></span>

<span data-ttu-id="075c5-125">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="075c5-126">추가 Azure 함수 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 함수 설명서](../functions-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="075c5-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
