---
title: "Azure CLI 스크립트 샘플 - Batch로 응용 프로그램 추가 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Batch로 응용 프로그램 추가"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="31342-103">Azure CLI를 사용하여 응용 프로그램을 Azure Batch에 추가</span><span class="sxs-lookup"><span data-stu-id="31342-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="31342-104">이 스크립트는 Azure Batch 풀 또는 작업에 사용할 응용 프로그램을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31342-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="31342-105">응용 프로그램을 설정하려면 실행 파일을 해당 종속성과 함께 .zip 파일로 패키지로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31342-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="31342-106">이 예제에서는 실행 가능한 zip 파일을 'my-application-exe.zip'이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="31342-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31342-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31342-107">Prerequisites</span></span>

- <span data-ttu-id="31342-108">아직 Azure CLI를 설치하지 않은 경우 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)에 있는 지침을 사용하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="31342-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="31342-109">아직 배치 계정이 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31342-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="31342-110">계정을 만드는 샘플 스크립트에 대한 [Azure CLI로 배치 계정 만들기](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31342-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="31342-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="31342-111">Sample script</span></span>

<span data-ttu-id="31342-112">[!code-azurecli[기본](../../../cli_scripts/batch/add-application/add-application.sh "응용 프로그램 추가")]</span><span class="sxs-lookup"><span data-stu-id="31342-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="31342-113">응용 프로그램 정리</span><span class="sxs-lookup"><span data-stu-id="31342-113">Clean up application</span></span>

<span data-ttu-id="31342-114">위의 샘플 스크립트를 실행한 후 다음 명령을 실행하여 응용 프로그램 및 업로드된 모든 응용 프로그램 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="31342-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="31342-115">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="31342-115">Script explanation</span></span>

<span data-ttu-id="31342-116">이 스크립트는 다음 명령을 사용하여 응용 프로그램을 만들고 응용 프로그램 패키지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="31342-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="31342-117">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="31342-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="31342-118">명령</span><span class="sxs-lookup"><span data-stu-id="31342-118">Command</span></span> | <span data-ttu-id="31342-119">참고 사항</span><span class="sxs-lookup"><span data-stu-id="31342-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="31342-120">az batch application create</span><span class="sxs-lookup"><span data-stu-id="31342-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="31342-121">응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31342-121">Creates an application.</span></span>  |
| [<span data-ttu-id="31342-122">az batch application set</span><span class="sxs-lookup"><span data-stu-id="31342-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="31342-123">응용 프로그램의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="31342-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="31342-124">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="31342-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="31342-125">지정된 응용 프로그램에 응용 프로그램 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31342-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="31342-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31342-126">Next steps</span></span>

<span data-ttu-id="31342-127">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31342-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="31342-128">추가 Batch CLI 스크립트 샘플은 [Azure Batch CLI 설명서](../batch-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31342-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
