---
title: "Azure CLI 스크립트 샘플 - VM 다시 시작 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 태그 및 ID로 VM 다시 시작"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: 4d0fe95287c91a4b656904f9007ceaaf866e155f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restart-vms"></a><span data-ttu-id="495ab-103">VM 다시 시작</span><span class="sxs-lookup"><span data-stu-id="495ab-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="495ab-104">이 샘플에서는 일부 VM을 가져와 다시 시작하는 몇 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-104">This sample shows a couple of ways to get some VMs and restart them.</span></span>

<span data-ttu-id="495ab-105">첫 번째 방법에서는 리소스 그룹의 모든 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-105">The first restarts all the VMs in the resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="495ab-106">두 번째 방법에서는 `az resouce list` 및 필터를 사용하여 태그가 지정된 VM을 리소스로 가져온 후 해당 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-106">The second gets the tagged VMs using `az resouce list` and filters to the resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="495ab-107">이 샘플은 Bash 셸에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="495ab-108">Windows 클라이언트에서 Azure CLI 스크립트 실행과 관련된 옵션은 [Windows에서 Azure CLI 실행](../windows/cli-options.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="495ab-108">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="495ab-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="495ab-109">Sample script</span></span>

<span data-ttu-id="495ab-110">이 샘플에는 세 가지 스크립트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-110">The sample has three scripts.</span></span>
<span data-ttu-id="495ab-111">첫 번째 스크립트는 가상 컴퓨터를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-111">The first one provisions the virtual machines.</span></span>
<span data-ttu-id="495ab-112">이 스크립트는 대기 없음 옵션을 사용하므로 명령은 각 VM이 프로비전할 때까지 대기하지 않고 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-112">It uses the no-wait option so the command returns without waiting on each VM to be provisioned.</span></span>
<span data-ttu-id="495ab-113">두 번째 스크립트는 VM이 완전히 프로비전될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-113">The second waits for the VMs to be fully provisioned.</span></span>
<span data-ttu-id="495ab-114">세 번째 스크립트는 프로비전된 모든 VM을 다시 시작한 다음, 태그가 지정된 VM만 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-114">The third script restarts all the VMs that were provisioned, and then just the tagged VMs.</span></span>

### <a name="provision-the-vms"></a><span data-ttu-id="495ab-115">VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="495ab-115">Provision the VMs</span></span>

<span data-ttu-id="495ab-116">이 스크립트는 리소스 그룹을 만든 다음 다시 시작할 세 개의 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-116">This script creates a resource group and then it creates three VMs to restart.</span></span>
<span data-ttu-id="495ab-117">그 중 두 개의 VM에 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-117">Two of them are tagged.</span></span>

<span data-ttu-id="495ab-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "VM 프로비전")]</span><span class="sxs-lookup"><span data-stu-id="495ab-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision the VMs")]</span></span>

### <a name="wait"></a><span data-ttu-id="495ab-119">Wait</span><span class="sxs-lookup"><span data-stu-id="495ab-119">Wait</span></span>

<span data-ttu-id="495ab-120">이 스크립트는 세 개의 VM이 모두 프로비전될 때까지 또는 그 중 하나가 프로비전되지 못할 때까지 20초마다 프로비저닝 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-120">This script checks on the provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails to provision.</span></span>

<span data-ttu-id="495ab-121">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "VM이 프로비전될 때까지 대기")]</span><span class="sxs-lookup"><span data-stu-id="495ab-121">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for the VMs to be provisioned")]</span></span>

### <a name="restart-the-vms"></a><span data-ttu-id="495ab-122">VM 다시 시작</span><span class="sxs-lookup"><span data-stu-id="495ab-122">Restart the VMs</span></span>

<span data-ttu-id="495ab-123">이 스크립트는 리소스 그룹의 모든 VM을 다시 시작한 다음, 태그가 지정된 VM만 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-123">This script restarts all the VMs in the resource group, and then it restarts just the tagged VMs.</span></span>

<span data-ttu-id="495ab-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "태그로 VM 다시 시작")]</span><span class="sxs-lookup"><span data-stu-id="495ab-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="495ab-125">배포 정리</span><span class="sxs-lookup"><span data-stu-id="495ab-125">Clean up deployment</span></span> 

<span data-ttu-id="495ab-126">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-126">After the script sample has been run, the following command can be used to remove the resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="495ab-127">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="495ab-127">Script explanation</span></span>

<span data-ttu-id="495ab-128">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-128">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="495ab-129">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-129">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="495ab-130">명령</span><span class="sxs-lookup"><span data-stu-id="495ab-130">Command</span></span> | <span data-ttu-id="495ab-131">참고 사항</span><span class="sxs-lookup"><span data-stu-id="495ab-131">Notes</span></span> |
|---|---|
| [<span data-ttu-id="495ab-132">az group create</span><span class="sxs-lookup"><span data-stu-id="495ab-132">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="495ab-133">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-133">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="495ab-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="495ab-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="495ab-135">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-135">Creates the virtual machines.</span></span>  |
| [<span data-ttu-id="495ab-136">az vm list</span><span class="sxs-lookup"><span data-stu-id="495ab-136">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="495ab-137">`--query`와 함께 사용되어 VM이 다시 시작된 후에 프로비전되도록 하고 VM ID를 가져와 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-137">Used with `--query` to ensure the VMs are provisioned before restarting them, and then to get the IDs of the VMs to restart them.</span></span> |
| [<span data-ttu-id="495ab-138">az resource list</span><span class="sxs-lookup"><span data-stu-id="495ab-138">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="495ab-139">`--query`와 함께 사용되어 태그를 사용하는 VM ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-139">Used with `--query` to get the IDs of the VMs using the tag.</span></span> |
| [<span data-ttu-id="495ab-140">az vm restart</span><span class="sxs-lookup"><span data-stu-id="495ab-140">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="495ab-141">VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-141">Restarts the VMs.</span></span> |
| [<span data-ttu-id="495ab-142">az group delete</span><span class="sxs-lookup"><span data-stu-id="495ab-142">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="495ab-143">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-143">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="495ab-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="495ab-144">Next steps</span></span>

<span data-ttu-id="495ab-145">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="495ab-145">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="495ab-146">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="495ab-146">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
