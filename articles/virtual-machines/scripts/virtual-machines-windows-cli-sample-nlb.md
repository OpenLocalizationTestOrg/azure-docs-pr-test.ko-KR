---
title: "Azure CLI 스크립트 샘플 - NLB를 사용하여 Windows Server 2016 VM 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - NLB를 사용하여 Windows Server 2016 VM 만들기"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: 916204d2b94868057b824feee7b7d032c66382f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="241ec-103">항상 사용 가능한 가상 컴퓨터 간에 트래픽 부하 분산</span><span class="sxs-lookup"><span data-stu-id="241ec-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="241ec-104">이 스크립트 샘플에서는 항상 사용 가능하고 부하 분산된 구성에서 구성된 여러 Ubuntu 가상 컴퓨터를 실행하는 데 필요한 모든 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="241ec-105">스크립트를 실행하면 3개의 가상 컴퓨터가 Azure 가용성 집합에 조인되고 Azure Load Balancer를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="241ec-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="241ec-106">Sample script</span></span>

<span data-ttu-id="241ec-107">[!code-azurecli-interactive[기본](../../../cli_scripts/virtual-machine/create-vm-nlb/create-windows-vm-nlb.sh "VM 빠른 생성")]</span><span class="sxs-lookup"><span data-stu-id="241ec-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-windows-vm-nlb.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="241ec-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="241ec-108">Clean up deployment</span></span> 

<span data-ttu-id="241ec-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="241ec-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="241ec-110">Script explanation</span></span>

<span data-ttu-id="241ec-111">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터, 가용성 집합, 부하 분산 장치 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="241ec-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="241ec-113">명령</span><span class="sxs-lookup"><span data-stu-id="241ec-113">Command</span></span> | <span data-ttu-id="241ec-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="241ec-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="241ec-115">az group create</span><span class="sxs-lookup"><span data-stu-id="241ec-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="241ec-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="241ec-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="241ec-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="241ec-118">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="241ec-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="241ec-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="241ec-120">고정 IP 주소 및 연결된 DNS 이름을 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="241ec-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="241ec-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="241ec-122">Azure NLB(Network Load Balancer)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-122">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="241ec-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="241ec-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="241ec-124">NLB 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-124">Creates an NLB probe.</span></span> <span data-ttu-id="241ec-125">NLB 프로브는 NLB 집합에서 각 VM을 모니터링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-125">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="241ec-126">모든 VM이 액세스할 수 없게 되면 트래픽은 VM에 라우팅되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="241ec-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="241ec-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="241ec-128">NLB 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-128">Creates an NLB rule.</span></span> <span data-ttu-id="241ec-129">이 샘플에서는 포트 80에 대한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="241ec-130">HTTP 트래픽이 NLB에 도착하면 NLB 집합에서 VM 중 하나인 포트 80에 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-130">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="241ec-131">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="241ec-131">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="241ec-132">NLB NAT(네트워크 주소 변환) 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-132">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="241ec-133">NAT 규칙은 VM에 있는 포트에 NLB의 포트를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-133">NAT rules map a port of the NLB to a port on a VM.</span></span> <span data-ttu-id="241ec-134">이 샘플에서는 NLB 집합의 각 VM에 SSH 트래픽에 대한 NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-134">In this sample, a NAT rule is created for SSH traffic to each VM in the NLB set.</span></span>  |
| [<span data-ttu-id="241ec-135">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="241ec-135">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="241ec-136">인터넷과 가상 컴퓨터 간에 보안 경계인 NSG(네트워크 보안 그룹)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-136">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="241ec-137">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="241ec-137">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="241ec-138">인바운드 트래픽을 허용하도록 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-138">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="241ec-139">이 샘플에서 SSH 트래픽에 대해 포트 22가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-139">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="241ec-140">az network nic create</span><span class="sxs-lookup"><span data-stu-id="241ec-140">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="241ec-141">가상 네트워크 카드를 만들고 가상 네트워크, 서브넷 및 NSG에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-141">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="241ec-142">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="241ec-142">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="241ec-143">가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-143">Creates an availability set.</span></span> <span data-ttu-id="241ec-144">가용성 집합을 사용하면 오류가 발생하는 경우 물리적 리소스 간에 가상 컴퓨터를 분산하여 응용 프로그램 가동 시간을 확인합니다. 전체 집합은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-144">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="241ec-145">az vm create</span><span class="sxs-lookup"><span data-stu-id="241ec-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="241ec-146">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 NSG에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="241ec-147">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="241ec-148">az group delete</span><span class="sxs-lookup"><span data-stu-id="241ec-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="241ec-149">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="241ec-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="241ec-150">Next steps</span></span>

<span data-ttu-id="241ec-151">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="241ec-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="241ec-152">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="241ec-152">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
