---
title: "Vm 다시 시작 스크립트 샘플 CLI-aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="9cee7-103">VM 다시 시작</span><span class="sxs-lookup"><span data-stu-id="9cee7-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="9cee7-104">이 샘플 몇 가지 방법으로 tooget 일부 Vm을 표시 하 고 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="9cee7-105">처음 hello hello 리소스 그룹에 모든 hello Vm 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="9cee7-106">hello 두 번째 가져옵니다 hello 태그가 지정 된 사용 하 여 Vm `az resouce list` 및 vm을 toohello 리소스를 필터링 하 고 해당 Vm을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="9cee7-107">이 샘플은 Bash 셸에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="9cee7-108">Windows 클라이언트에서 Azure CLI 스크립트를 실행 하는 옵션에 대 한 참조 [hello Azure CLI Windows에서 실행 중인](../windows/cli-options.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="9cee7-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="9cee7-109">Sample script</span></span>

<span data-ttu-id="9cee7-110">hello 샘플에는 세 가지 스크립트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-110">hello sample has three scripts.</span></span>
<span data-ttu-id="9cee7-111">첫 번째 hello 가상 컴퓨터를 프로비저닝하고 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="9cee7-112">Hello 명령은 각 VM toobe 프로 비전에 대기 하지 않고 반환 하므로 hello 아니요 대기 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="9cee7-113">두 번째 hello hello Vm toobe 완전히 프로 비전을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="9cee7-114">세 번째 스크립트 hello를 프로 비전 된 모든 hello Vm 다시 시작 하 고 정당한 hello 태그가 Vm을 지정 하는 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="9cee7-115">Hello Vm을 프로 비전</span><span class="sxs-lookup"><span data-stu-id="9cee7-115">Provision hello VMs</span></span>

<span data-ttu-id="9cee7-116">이 스크립트 리소스 그룹을 만들고 세 개의 Vm toorestart 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="9cee7-117">그 중 두 개의 VM에 태그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="9cee7-118">Wait</span><span class="sxs-lookup"><span data-stu-id="9cee7-118">Wait</span></span>

<span data-ttu-id="9cee7-119">이 스크립트는 hello tooprovision 실패 둘 중 하나 또는 모두 세 개의 Vm이 프로 비전 될 때까지 20 초 마다 프로 비전 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="9cee7-120">Hello Vm을 다시 시작</span><span class="sxs-lookup"><span data-stu-id="9cee7-120">Restart hello VMs</span></span>

<span data-ttu-id="9cee7-121">이 스크립트는 모든 hello Vm hello 리소스 그룹에서 다시 시작 하 고 방금 hello 태그가 지정 된 Vm을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9cee7-122">배포 정리</span><span class="sxs-lookup"><span data-stu-id="9cee7-122">Clean up deployment</span></span> 

<span data-ttu-id="9cee7-123">Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, Vm 및 관련 된 모든 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9cee7-124">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="9cee7-124">Script explanation</span></span>

<span data-ttu-id="9cee7-125">이 스크립트 명령 toocreate 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="9cee7-126">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9cee7-127">명령</span><span class="sxs-lookup"><span data-stu-id="9cee7-127">Command</span></span> | <span data-ttu-id="9cee7-128">참고 사항</span><span class="sxs-lookup"><span data-stu-id="9cee7-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9cee7-129">az group create</span><span class="sxs-lookup"><span data-stu-id="9cee7-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9cee7-130">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9cee7-131">az vm create</span><span class="sxs-lookup"><span data-stu-id="9cee7-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="9cee7-132">Hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="9cee7-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="9cee7-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="9cee7-134">함께 사용할 `--query` tooensure hello Vm을 다시 시작 하기 전에 프로 비전 하 고 다음 tooget hello hello Vm toorestart의 Id를 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="9cee7-135">az resource list</span><span class="sxs-lookup"><span data-stu-id="9cee7-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="9cee7-136">함께 사용할 `--query` tooget hello hello 태그를 사용 하 여 hello Vm의 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="9cee7-137">az vm restart</span><span class="sxs-lookup"><span data-stu-id="9cee7-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="9cee7-138">Hello Vm을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="9cee7-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="9cee7-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9cee7-140">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9cee7-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cee7-141">Next steps</span></span>

<span data-ttu-id="9cee7-142">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9cee7-143">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cee7-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
