---
title: "Azure Storage에 연결하는 Azure Function 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Azure Storage에 연결하는 Azure Function 만들기"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="ac5ac-103">Azure Storage 계정에 함수 앱 통합</span><span class="sxs-lookup"><span data-stu-id="ac5ac-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="ac5ac-104">이 샘플 스크립트는 함수 앱 및 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ac5ac-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ac5ac-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ac5ac-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ac5ac-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ac5ac-108">Sample script</span></span>

<span data-ttu-id="ac5ac-109">이 샘플은 Azure 함수 앱을 만들고 앱 설정에 저장소 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-109">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

<span data-ttu-id="ac5ac-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Azure Storage 계정에 함수 앱 통합")]</span><span class="sxs-lookup"><span data-stu-id="ac5ac-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="ac5ac-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ac5ac-111">Clean up deployment</span></span>

<span data-ttu-id="ac5ac-112">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, App Service 앱 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-112">After the script sample has been run, the following command can be used to remove the resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ac5ac-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ac5ac-113">Script explanation</span></span>

<span data-ttu-id="ac5ac-114">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-114">This script uses the following commands.</span></span> <span data-ttu-id="ac5ac-115">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ac5ac-116">명령</span><span class="sxs-lookup"><span data-stu-id="ac5ac-116">Command</span></span> | <span data-ttu-id="ac5ac-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ac5ac-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ac5ac-118">az login</span><span class="sxs-lookup"><span data-stu-id="ac5ac-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="ac5ac-119">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="ac5ac-119">Login to Azure.</span></span> |
| [<span data-ttu-id="ac5ac-120">az group create</span><span class="sxs-lookup"><span data-stu-id="ac5ac-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ac5ac-121">위치와 함께 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ac5ac-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="ac5ac-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="ac5ac-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="ac5ac-123">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ac5ac-123">Create a storage account</span></span> |
| [<span data-ttu-id="ac5ac-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="ac5ac-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="ac5ac-125">새로운 함수 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ac5ac-125">Create a new function app</span></span> |
| [<span data-ttu-id="ac5ac-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="ac5ac-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="ac5ac-127">정리</span><span class="sxs-lookup"><span data-stu-id="ac5ac-127">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac5ac-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac5ac-128">Next steps</span></span>

<span data-ttu-id="ac5ac-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ac5ac-130">추가 Azure Functions CLI 스크립트 샘플은 [Azure Functions 설명서](../functions-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5ac-130">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
