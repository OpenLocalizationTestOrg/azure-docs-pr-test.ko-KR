---
title: "Azure CLI 스크립트 샘플 - Batch에서 풀 관리 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Batch에서 풀 관리"
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
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="364ba-103">Azure CLI를 사용하여 Azure Batch 풀 관리</span><span class="sxs-lookup"><span data-stu-id="364ba-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="364ba-104">다음 스크립트는 Azure Batch 서비스에서 계산 노드의 풀을 만들고 관리하기 위해 Azure CLI에서 사용 가능한 몇 가지 도구를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="364ba-105">샘플에 있는 명령은 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-105">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="364ba-106">VM을 실행하면 계정에 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-106">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="364ba-107">이러한 요금을 최소화하려면 샘플 실행을 완료한 후 VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-107">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="364ba-108">[풀 정리](#clean-up-pools)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364ba-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="364ba-109">Batch 풀은 Cloud Services 구성(Windows 전용)이나 Virtual Machine 구성(Windows 및 Linux)의 두 가지 방법을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="364ba-110">아래 샘플 스크립트는 두 가지 구성으로 풀을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-110">The sample scripts below show how to create pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="364ba-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="364ba-111">Prerequisites</span></span>

- <span data-ttu-id="364ba-112">아직 Azure CLI를 설치하지 않은 경우 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)에 있는 지침을 사용하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-112">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="364ba-113">아직 배치 계정이 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="364ba-114">계정을 만드는 샘플 스크립트에 대한 [Azure CLI로 배치 계정 만들기](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364ba-114">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="364ba-115">시작 작업에서 실행할 응용 프로그램을 아직 구성하지 않은 경우 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-115">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="364ba-116">응용 프로그램을 만들고 Azure에 응용 프로그램 패키지를 업로드하는 샘플 스크립트는 [Azure CLI를 사용하여 응용 프로그램을 Azure 배치에 추가](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364ba-116">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="364ba-117">클라우드 서비스 구성이 있는 풀 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="364ba-117">Pool with cloud service configuration sample script</span></span>

<span data-ttu-id="364ba-118">[!code-azurecli[메인](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "클라우드 서비스 풀 관리")]</span><span class="sxs-lookup"><span data-stu-id="364ba-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]</span></span>

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="364ba-119">가상 컴퓨터 구성이 있는 풀 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="364ba-119">Pool with virtual machine configuration sample script</span></span>

<span data-ttu-id="364ba-120">[!code-azurecli[메인](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "가상 컴퓨터 풀 관리")]</span><span class="sxs-lookup"><span data-stu-id="364ba-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]</span></span>

## <a name="clean-up-pools"></a><span data-ttu-id="364ba-121">풀 정리</span><span class="sxs-lookup"><span data-stu-id="364ba-121">Clean up pools</span></span>

<span data-ttu-id="364ba-122">위의 샘플 스크립트를 실행한 후 다음 명령을 실행하여 풀을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-122">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="364ba-123">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="364ba-123">Script explanation</span></span>

<span data-ttu-id="364ba-124">이 스크립트는 다음 명령을 사용하여 Batch 풀을 만들고 조작합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-124">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="364ba-125">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-125">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="364ba-126">명령</span><span class="sxs-lookup"><span data-stu-id="364ba-126">Command</span></span> | <span data-ttu-id="364ba-127">참고 사항</span><span class="sxs-lookup"><span data-stu-id="364ba-127">Notes</span></span> |
|---|---|
| [<span data-ttu-id="364ba-128">az batch account login</span><span class="sxs-lookup"><span data-stu-id="364ba-128">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="364ba-129">배치 계정에 대해 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-129">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="364ba-130">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="364ba-130">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="364ba-131">배치 계정에 사용 가능한 응용 프로그램을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-131">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="364ba-132">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="364ba-132">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="364ba-133">VM의 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-133">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="364ba-134">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="364ba-134">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="364ba-135">풀의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-135">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="364ba-136">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="364ba-136">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="364ba-137">사용 가능한 노드 에이전트 SKU 및 이미지 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-137">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="364ba-138">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="364ba-138">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="364ba-139">지정된 풀에서 실행 중인 VM 수의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-139">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="364ba-140">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="364ba-140">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="364ba-141">풀의 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-141">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="364ba-142">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="364ba-142">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="364ba-143">지정된 풀을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-143">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="364ba-144">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="364ba-144">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="364ba-145">풀에서 자동 확장을 사용하고 수식을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-145">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="364ba-146">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="364ba-146">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="364ba-147">풀에서 자동 확장을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-147">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="364ba-148">az batch node list</span><span class="sxs-lookup"><span data-stu-id="364ba-148">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="364ba-149">지정된 풀에서 계산 노드를 모두 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-149">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="364ba-150">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="364ba-150">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="364ba-151">지정된 계산 노드를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-151">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="364ba-152">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="364ba-152">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="364ba-153">지정된 풀에서 나열된 노드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-153">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="364ba-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="364ba-154">Next steps</span></span>

<span data-ttu-id="364ba-155">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="364ba-155">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="364ba-156">추가 Batch CLI 스크립트 샘플은 [Azure Batch CLI 설명서](../batch-cli-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="364ba-156">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

