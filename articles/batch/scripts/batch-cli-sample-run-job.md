---
title: "aaaAzure CLI 스크립트 샘플-일괄 처리 작업을 실행 합니다. | Microsoft Docs"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="97380-103">Azure CLI를 사용하여 Azure Batch에서 실행 중인 작업</span><span class="sxs-lookup"><span data-stu-id="97380-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="97380-104">이 스크립트 일괄 처리 작업을 만들고 추가 하는 일련의 작업 toohello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="97380-105">에 대해서도 설명 방법을 toomonitor 작업 및 작업.</span><span class="sxs-lookup"><span data-stu-id="97380-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="97380-106">마지막으로, tooquery 효율적으로 hello 작업의 작업에 대 한 정보에 대 한 일괄 처리 서비스 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="97380-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97380-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="97380-107">Prerequisites</span></span>

- <span data-ttu-id="97380-108">설치 hello hello에 제공 된 hello 지침을 사용 하 여 Azure CLI [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)아직 수행 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="97380-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="97380-109">아직 배치 계정이 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97380-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="97380-110">참조 [hello Azure CLI 일괄 처리 계정을 만들고](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) 가 계정을 만들고 하는 예제 스크립트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="97380-111">아직 수행 하지 않은 경우에 시작 작업에서 응용 프로그램 toorun 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="97380-112">참조 [응용 프로그램 tooAzure Azure CLI 포함 된 일괄 처리 추가](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) 응용 프로그램을 만들고 응용 프로그램 패키지 tooAzure 업로드 하는 예제 스크립트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="97380-113">작업을 실행 하는 hello에 풀을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="97380-114">클라우드 서비스 구성 또는 가상 컴퓨터 구성으로 풀을 만드는 샘플 스크립트는 [Azure CLI를 사용한 Azure 배치 풀 관리](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97380-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="97380-115">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="97380-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="97380-116">작업 정리</span><span class="sxs-lookup"><span data-stu-id="97380-116">Clean up job</span></span>

<span data-ttu-id="97380-117">Hello 위의 샘플 스크립트를 실행 한 후 작업 및 작업의 모든 명령을 tooremove 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="97380-118">Hello 풀 별도로 삭제 toobe 필요 함을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="97380-119">풀 만들기 및 삭제에 대한 자세한 내용은 [Azure CLI를 사용한 Azure 배치 풀 관리](./batch-cli-sample-manage-pool.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97380-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="97380-120">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="97380-120">Script explanation</span></span>

<span data-ttu-id="97380-121">이 스크립트는 일괄 작업 및 작업 명령을 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="97380-122">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="97380-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="97380-123">명령</span><span class="sxs-lookup"><span data-stu-id="97380-123">Command</span></span> | <span data-ttu-id="97380-124">참고 사항</span><span class="sxs-lookup"><span data-stu-id="97380-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="97380-125">az batch account login</span><span class="sxs-lookup"><span data-stu-id="97380-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="97380-126">배치 계정에 대해 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="97380-127">az batch job create</span><span class="sxs-lookup"><span data-stu-id="97380-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="97380-128">배치 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97380-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="97380-129">az batch job set</span><span class="sxs-lookup"><span data-stu-id="97380-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="97380-130">Batch 작업의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="97380-131">az batch job show</span><span class="sxs-lookup"><span data-stu-id="97380-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="97380-132">지정된 Batch 작업의 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="97380-133">az batch task create</span><span class="sxs-lookup"><span data-stu-id="97380-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="97380-134">추가 작업 toohello 일괄 작업을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="97380-135">az batch task show</span><span class="sxs-lookup"><span data-stu-id="97380-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="97380-136">Hello에서 작업의 검색 hello 세부 정보 일괄 작업을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="97380-137">az batch task list</span><span class="sxs-lookup"><span data-stu-id="97380-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="97380-138">Hello ְ  ¾ hello 지정 된 작업을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="97380-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97380-139">Next steps</span></span>

<span data-ttu-id="97380-140">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="97380-141">추가 일괄 처리 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 일괄 처리 CLI 설명서](../batch-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="97380-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
