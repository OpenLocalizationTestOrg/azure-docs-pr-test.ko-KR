---
title: "aaaAzure CLI 스크립트 샘플-일괄 처리의 풀 관리 | Microsoft Docs"
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="6456d-103">Azure CLI를 사용하여 Azure Batch 풀 관리</span><span class="sxs-lookup"><span data-stu-id="6456d-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="6456d-104">이러한 스크립트 hello Azure CLI toocreate에서 사용할 수 있는 hello 도구 중 일부를 보여 주고 hello Azure 배치 서비스에서 계산 노드는 풀을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="6456d-105">이 샘플의 hello 명령은 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="6456d-106">실행 중인 Vm 요금 tooyour 계정을 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="6456d-107">toominimize 이러한 요금 hello 샘플 실행을 완료 하 고 나면 hello Vm을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="6456d-108">[풀 정리](#clean-up-pools)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6456d-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="6456d-109">Batch 풀은 Cloud Services 구성(Windows 전용)이나 Virtual Machine 구성(Windows 및 Linux)의 두 가지 방법을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="6456d-110">아래의 hello 샘플 스크립트는 두 구성으로 toocreate 풀링 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6456d-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6456d-111">Prerequisites</span></span>

- <span data-ttu-id="6456d-112">설치 hello hello에 제공 된 hello 지침을 사용 하 여 Azure CLI [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)아직 수행 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="6456d-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="6456d-113">아직 배치 계정이 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="6456d-114">참조 [hello Azure CLI 일괄 처리 계정을 만들고](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) 가 계정을 만들고 하는 예제 스크립트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="6456d-115">아직 수행 하지 않은 경우에 시작 작업에서 응용 프로그램 toorun 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="6456d-116">참조 [응용 프로그램 tooAzure Azure CLI 포함 된 일괄 처리 추가](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) 응용 프로그램을 만들고 응용 프로그램 패키지 tooAzure 업로드 하는 예제 스크립트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="6456d-117">클라우드 서비스 구성이 있는 풀 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="6456d-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="6456d-118">가상 컴퓨터 구성이 있는 풀 샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="6456d-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="6456d-119">풀 정리</span><span class="sxs-lookup"><span data-stu-id="6456d-119">Clean up pools</span></span>

<span data-ttu-id="6456d-120">Hello 위의 샘플 스크립트를 실행 한 후 다음 명령 toodelete hello 풀 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="6456d-121">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="6456d-121">Script explanation</span></span>

<span data-ttu-id="6456d-122">이 스크립트는 다음 명령을 toocreate hello를 사용 하 여 하 고 일괄 처리 풀 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="6456d-123">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="6456d-124">명령</span><span class="sxs-lookup"><span data-stu-id="6456d-124">Command</span></span> | <span data-ttu-id="6456d-125">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6456d-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6456d-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="6456d-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="6456d-127">배치 계정에 대해 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="6456d-128">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="6456d-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="6456d-129">Hello hello 일괄 처리 계정에에서 사용 가능한 응용 프로그램을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="6456d-130">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="6456d-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="6456d-131">VM의 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="6456d-132">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="6456d-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="6456d-133">풀의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="6456d-134">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="6456d-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="6456d-135">사용 가능한 노드 에이전트 SKU 및 이미지 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="6456d-136">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="6456d-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="6456d-137">Hello에 실행 중인 Vm의 크기 조정 hello 번호 풀을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="6456d-138">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="6456d-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="6456d-139">풀의 hello 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="6456d-140">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="6456d-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="6456d-141">지정 된 hello 삭제 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="6456d-142">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="6456d-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="6456d-143">풀에서 자동 확장을 사용하고 수식을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="6456d-144">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="6456d-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="6456d-145">풀에서 자동 확장을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="6456d-146">az batch node list</span><span class="sxs-lookup"><span data-stu-id="6456d-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="6456d-147">모든 나열 hello에 hello 계산 노드가 풀을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="6456d-148">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="6456d-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="6456d-149">Hello 지정 된 계산 노드를 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="6456d-150">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="6456d-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="6456d-151">Hello에서 delete 나열 된 hello 노드 풀을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="6456d-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6456d-152">Next steps</span></span>

<span data-ttu-id="6456d-153">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6456d-154">추가 일괄 처리 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 일괄 처리 CLI 설명서](../batch-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6456d-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

