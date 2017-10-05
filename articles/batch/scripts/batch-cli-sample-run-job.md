---
title: "Azure CLI 스크립트 샘플 - Batch로 작업 실행 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Batch로 작업 실행"
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
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="3d183-103">Azure CLI를 사용하여 Azure Batch에서 실행 중인 작업</span><span class="sxs-lookup"><span data-stu-id="3d183-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="3d183-104">이 스크립트는 Batch 작업을 만들고 일련의 태스크를 작업에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="3d183-105">또한 작업 및 태스크를 모니터링하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-105">It also demonstrates how to monitor a job and its tasks.</span></span> <span data-ttu-id="3d183-106">마지막으로, 작업 관련 정보에 대한 배치 서비스를 효과적으로 쿼리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-106">Finally, it shows how to query the Batch service efficiently for information about the job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d183-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3d183-107">Prerequisites</span></span>

- <span data-ttu-id="3d183-108">아직 Azure CLI를 설치하지 않은 경우 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)에 있는 지침을 사용하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="3d183-109">아직 배치 계정이 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="3d183-110">계정을 만드는 샘플 스크립트에 대한 [Azure CLI로 배치 계정 만들기](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d183-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="3d183-111">시작 작업에서 실행할 응용 프로그램을 아직 구성하지 않은 경우 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-111">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="3d183-112">응용 프로그램을 만들고 Azure에 응용 프로그램 패키지를 업로드하는 샘플 스크립트는 [Azure CLI를 사용하여 응용 프로그램을 Azure 배치에 추가](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d183-112">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>
- <span data-ttu-id="3d183-113">작업이 실행될 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-113">Configure a pool on which the job will run.</span></span> <span data-ttu-id="3d183-114">클라우드 서비스 구성 또는 가상 컴퓨터 구성으로 풀을 만드는 샘플 스크립트는 [Azure CLI를 사용한 Azure 배치 풀 관리](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d183-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="3d183-115">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3d183-115">Sample script</span></span>

<span data-ttu-id="3d183-116">[!code-azurecli[메인](../../../cli_scripts/batch/run-job/run-job.sh "작업 실행")]</span><span class="sxs-lookup"><span data-stu-id="3d183-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]</span></span>

## <a name="clean-up-job"></a><span data-ttu-id="3d183-117">작업 정리</span><span class="sxs-lookup"><span data-stu-id="3d183-117">Clean up job</span></span>

<span data-ttu-id="3d183-118">위의 샘플 스크립트를 실행한 후 다음 명령을 실행하여 작업 및 작업의 모든 태스크를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-118">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="3d183-119">풀은 별도로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-119">Note that the pool will need to be deleted separately.</span></span> <span data-ttu-id="3d183-120">풀 만들기 및 삭제에 대한 자세한 내용은 [Azure CLI를 사용한 Azure 배치 풀 관리](./batch-cli-sample-manage-pool.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d183-120">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="3d183-121">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3d183-121">Script explanation</span></span>

<span data-ttu-id="3d183-122">이 스크립트는 다음 명령을 사용하여 Batch 작업 및 태스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-122">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="3d183-123">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-123">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="3d183-124">명령</span><span class="sxs-lookup"><span data-stu-id="3d183-124">Command</span></span> | <span data-ttu-id="3d183-125">참고 사항</span><span class="sxs-lookup"><span data-stu-id="3d183-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d183-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="3d183-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="3d183-127">배치 계정에 대해 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="3d183-128">az batch job create</span><span class="sxs-lookup"><span data-stu-id="3d183-128">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="3d183-129">배치 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-129">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="3d183-130">az batch job set</span><span class="sxs-lookup"><span data-stu-id="3d183-130">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="3d183-131">Batch 작업의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-131">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="3d183-132">az batch job show</span><span class="sxs-lookup"><span data-stu-id="3d183-132">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="3d183-133">지정된 Batch 작업의 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-133">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="3d183-134">az batch task create</span><span class="sxs-lookup"><span data-stu-id="3d183-134">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="3d183-135">지정된 Batch 작업에 태스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-135">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="3d183-136">az batch task show</span><span class="sxs-lookup"><span data-stu-id="3d183-136">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="3d183-137">지정된 Batch 작업에서 태스크의 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-137">Retrieves the details of a task from the specified Batch job.</span></span>  |
| [<span data-ttu-id="3d183-138">az batch task list</span><span class="sxs-lookup"><span data-stu-id="3d183-138">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="3d183-139">지정된 작업과 연관된 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-139">Lists the tasks associated with the specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="3d183-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d183-140">Next steps</span></span>

<span data-ttu-id="3d183-141">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d183-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3d183-142">추가 Batch CLI 스크립트 샘플은 [Azure Batch CLI 설명서](../batch-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d183-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
