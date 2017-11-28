---
title: "CLI 스크립트 샘플-aaaAzure nlb 기능이 있는 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - NLB를 사용하여 Linux VM 만들기"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 79b245c1268734fead313b34c120f74ab2330d4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-highly-available-vm"></a><span data-ttu-id="62dc9-103">항상 사용 가능한 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="62dc9-103">Create a highly available VM</span></span>

<span data-ttu-id="62dc9-104">이 스크립트 예제에서는 필요한 모든 것을 만듭니다 toorun 여러 Ubuntu 가상 컴퓨터에서 항상 사용 가능한 구성 및 부하 분산 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="62dc9-105">Hello 스크립트를 실행 한 후 3 개의 가상 컴퓨터가 Azure 가용성 집합에 가입된 tooan 될 것 이며는 Azure 부하 분산 장치를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="62dc9-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="62dc9-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="62dc9-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="62dc9-107">Clean up deployment</span></span> 

<span data-ttu-id="62dc9-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="62dc9-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="62dc9-109">Script explanation</span></span>

<span data-ttu-id="62dc9-110">이 스크립트 명령 toocreate 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="62dc9-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="62dc9-112">명령</span><span class="sxs-lookup"><span data-stu-id="62dc9-112">Command</span></span> | <span data-ttu-id="62dc9-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="62dc9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="62dc9-114">az group create</span><span class="sxs-lookup"><span data-stu-id="62dc9-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="62dc9-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="62dc9-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="62dc9-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="62dc9-117">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="62dc9-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="62dc9-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="62dc9-119">고정 IP 주소 및 연결된 DNS 이름을 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="62dc9-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="62dc9-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="62dc9-121">Azure NLB(Network Load Balancer)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-121">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="62dc9-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="62dc9-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="62dc9-123">NLB 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-123">Creates an NLB probe.</span></span> <span data-ttu-id="62dc9-124">NLB 프로브는 사용 되는 toomonitor hello NLB 집합의 각 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-124">An NLB probe is used toomonitor each VM in hello NLB set.</span></span> <span data-ttu-id="62dc9-125">모든 VM에 액세스할 수 없게 됩니다, 트래픽 라우팅된 toohello VM 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="62dc9-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="62dc9-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="62dc9-127">NLB 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-127">Creates an NLB rule.</span></span> <span data-ttu-id="62dc9-128">이 샘플에서는 포트 80에 대한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="62dc9-129">HTTP 트래픽을 hello NLB에 도착 하면 때 라우트된 tooport 80 hello NLB 집합의 hello Vm 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-129">As HTTP traffic arrives at hello NLB, it is routed tooport 80 one of hello VMs in hello NLB set.</span></span> |
| [<span data-ttu-id="62dc9-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="62dc9-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="62dc9-131">NLB NAT(네트워크 주소 변환) 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-131">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="62dc9-132">NAT 규칙 hello VM에서 NLB tooa 포트의 포트를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-132">NAT rules map a port of hello NLB tooa port on a VM.</span></span> <span data-ttu-id="62dc9-133">이 샘플에서는 SSH hello NLB 집합에 트래픽 tooeach VM에 대 한 NAT 규칙 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello NLB set.</span></span>  |
| [<span data-ttu-id="62dc9-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="62dc9-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="62dc9-135">Hello 인터넷 및 hello 가상 컴퓨터 간의 보안 경계를 네트워크 보안 그룹 (NSG)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="62dc9-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="62dc9-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="62dc9-137">NSG 규칙 tooallow 만듭니다 트래픽 인바운드 합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="62dc9-138">이 샘플에서 SSH 트래픽에 대해 포트 22가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="62dc9-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="62dc9-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="62dc9-140">가상 네트워크 카드를 만들고 toohello 가상 네트워크, 서브넷 및 NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="62dc9-141">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="62dc9-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="62dc9-142">가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-142">Creates an availability set.</span></span> <span data-ttu-id="62dc9-143">가용성 집합으로 오류가 발생 하면 전체 집합 hello 영향을 받지 않습니다 되도록 hello 가상 컴퓨터는 실제 리소스 분배 하 여 응용 프로그램의 가동 시간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="62dc9-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="62dc9-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="62dc9-145">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="62dc9-146">이 명령을 사용 하는 hello 가상 컴퓨터 이미지 toobe 지정 및 관리 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="62dc9-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="62dc9-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="62dc9-148">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="62dc9-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="62dc9-149">Next steps</span></span>

<span data-ttu-id="62dc9-150">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="62dc9-151">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="62dc9-151">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
