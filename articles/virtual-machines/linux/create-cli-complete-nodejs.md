---
title: "Azure CLI 1.0을 사용하여 전체 Linux 환경 만들기 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 저장소, Linux VM, 가상 네트워크 및 서브넷, 부하 분산 장치, NIC, 공용 IP, 네트워크 보안 그룹을 모두 처음부터 새로 만듭니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 201ccd523e49d638ace50fbc0ffdceb705b35473
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-10"></a><span data-ttu-id="3bb71-103">Azure CLI 1.0을 사용하여 전체 Linux 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-103">Create a complete Linux environment with the Azure CLI 1.0</span></span>
<span data-ttu-id="3bb71-104">이 문서에서는 개발 및 간단한 계산에 유용한 부하 분산 장치와 한 쌍의 VM을 사용하여 간단한 네트워크를 빌드해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="3bb71-105">인터넷 어디에서나 안전하게 실행되는 두 개의 Linux VM에 연결할 수 있을 때까지 프로세스를 명령별로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="3bb71-106">그 후에는 좀 더 복잡한 네트워크 및 환경으로 넘어갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-106">Then you can move on to more complex networks and environments.</span></span>

<span data-ttu-id="3bb71-107">그 과정에서 Resource Manager 배포 모델이 제공하는 종속성 계층 구조와 강력한 기능을 이해할 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="3bb71-108">시스템이 빌드되는 방식을 이해하면 [Azure Resource Manager 템플릿](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 사용하여 시스템을 훨씬 더 빠르게 다시 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3bb71-109">또한 환경의 여러 부분이 서로 어떻게 연결되는지 파악하고 나면 이러한 환경 부분을 자동화하는 템플릿을 더 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="3bb71-110">환경에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-110">The environment contains:</span></span>

* <span data-ttu-id="3bb71-111">가용성 집합에 포함된 두 VM</span><span class="sxs-lookup"><span data-stu-id="3bb71-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="3bb71-112">포트 80에서 부하 분산 규칙이 있는 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="3bb71-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="3bb71-113">원치 않는 트래픽으로부터 VM을 보호하기 위한 NSG(네트워크 보안 그룹) 규칙</span><span class="sxs-lookup"><span data-stu-id="3bb71-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

<span data-ttu-id="3bb71-114">이러한 사용자 지정 환경을 만들려면 Resource Manager 모드(`azure config mode arm`)의 최신 [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-114">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="3bb71-115">JSON 구문 분석 도구도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="3bb71-116">이 예제에서는 [jq](https://stedolan.github.io/jq/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="3bb71-117">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="3bb71-117">CLI versions to complete the task</span></span>
<span data-ttu-id="3bb71-118">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-118">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="3bb71-119">[Azure CLI 1.0](#quick-commands) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="3bb71-119">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3bb71-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="3bb71-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="3bb71-121">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="3bb71-121">Quick commands</span></span>
<span data-ttu-id="3bb71-122">작업을 빠르게 완료해야 하는 경우 다음 섹션에서 Azure에 VM을 업로드하는 기본 명령에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="3bb71-122">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="3bb71-123">각 단계에 대한 보다 자세한 내용 및 상황 설명은 [여기](#detailed-walkthrough)서부터 문서 끝까지 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb71-123">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="3bb71-124">[Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 로그인하여 Resource Manager 모드를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-124">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="3bb71-125">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-125">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3bb71-126">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="3bb71-127">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-127">Create the resource group.</span></span> <span data-ttu-id="3bb71-128">다음 예제에서는 `westeurope` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-128">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="3bb71-129">JSON 파서를 사용하여 리소스 그룹을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-129">Verify the resource group by using the JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="3bb71-130">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-130">Create the storage account.</span></span> <span data-ttu-id="3bb71-131">다음 예제에서는 `mystorageaccount`라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-131">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="3bb71-132">(저장소 계정 이름은 고유해야 하므로 자신만의 이름을 제공하세요.)</span><span class="sxs-lookup"><span data-stu-id="3bb71-132">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="3bb71-133">JSON 파서를 사용하여 저장소 계정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-133">Verify the storage account by using the JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="3bb71-134">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-134">Create the virtual network.</span></span> <span data-ttu-id="3bb71-135">다음 예제는 `myVnet`이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-135">The following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="3bb71-136">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-136">Create a subnet.</span></span> <span data-ttu-id="3bb71-137">다음 예제는 `mySubnet`이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-137">The following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="3bb71-138">JSON 파서를 사용하여 가상 네트워크 및 서브넷을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-138">Verify the virtual network and subnet by using the JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="3bb71-139">공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-139">Create a public IP.</span></span> <span data-ttu-id="3bb71-140">다음 예제는 `mypublicdns`라는 DNS 이름으로 `myPublicIP`라는 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-140">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="3bb71-141">DNS 이름은 고유해야 하므로 자신만의 이름을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb71-141">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="3bb71-142">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-142">Create the load balancer.</span></span> <span data-ttu-id="3bb71-143">다음 예제는 `myLoadBalancer`라는 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-143">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="3bb71-144">부하 분산 장치에 대한 프런트 엔드 IP 풀을 만들고 공용 IP에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-144">Create a front-end IP pool for the load balancer, and associate the public IP.</span></span> <span data-ttu-id="3bb71-145">다음 예제는 `mySubnetPool`이라는 프런트 엔드 IP 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-145">The following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="3bb71-146">부하 분산 장치에 대한 백 엔드 IP 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-146">Create the back-end IP pool for the load balancer.</span></span> <span data-ttu-id="3bb71-147">다음 예제는 `myBackEndPool`이라는 백 엔드 IP 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-147">The following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="3bb71-148">부하 분산 장치에 대한 SSH 인바운드 NAT(Network Address Translation) 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-148">Create SSH inbound network address translation (NAT) rules for the load balancer.</span></span> <span data-ttu-id="3bb71-149">다음 예제는 `myLoadBalancerRuleSSH1` 및 `myLoadBalancerRuleSSH2`라는 두 개의 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-149">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="3bb71-150">부하 분산 장치에 대한 웹 인바운드 NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-150">Create the web inbound NAT rules for the load balancer.</span></span> <span data-ttu-id="3bb71-151">다음 예제는 `myLoadBalancerRuleWeb`이라는 부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-151">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="3bb71-152">부하 분산 장치 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-152">Create the load balancer health probe.</span></span> <span data-ttu-id="3bb71-153">다음 예제에는 `myHealthProbe`라는 TCP 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-153">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="3bb71-154">JSON 파서를 사용하여 부하 분산 장치, IP 풀, NAT 규칙을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-154">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="3bb71-155">첫 번째 NIC(네트워크 인터페이스 카드)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-155">Create the first network interface card (NIC).</span></span> <span data-ttu-id="3bb71-156">`#####-###-###` 섹션을 Azure 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-156">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="3bb71-157">만드는 리소스를 검사할 때 구독 ID가 **jq** 출력에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-157">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span></span> <span data-ttu-id="3bb71-158">`azure account list`를 사용하여 구독 ID를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="3bb71-159">다음 예제는 `myNic1`이라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-159">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="3bb71-160">두 번째 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-160">Create the second NIC.</span></span> <span data-ttu-id="3bb71-161">다음 예제는 `myNic2`라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-161">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="3bb71-162">JSON 파서를 사용하여 두 개의 NIC를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-162">Verify the two NICs by using the JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="3bb71-163">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-163">Create the network security group.</span></span> <span data-ttu-id="3bb71-164">다음 예제에서는 `myNetworkSecurityGroup`이라는 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-164">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="3bb71-165">네트워크 보안 그룹에 대해 인바운드 규칙을 두 개 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-165">Add two inbound rules for the network security group.</span></span> <span data-ttu-id="3bb71-166">다음 예제는 `myNetworkSecurityGroupRuleSSH` 및 `myNetworkSecurityGroupRuleHTTP`라는 두 개의 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-166">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="3bb71-167">JSON 파서를 사용하여 네트워크 보안 그룹 및 인바운드 규칙을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-167">Verify the network security group and inbound rules by using the JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="3bb71-168">네트워크 보안 그룹을 두 개의 NIC에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-168">Bind the network security group to the two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="3bb71-169">가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-169">Create the availability set.</span></span> <span data-ttu-id="3bb71-170">다음 예제는 `myAvailabilitySet`라는 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-170">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="3bb71-171">첫 번째 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-171">Create the first Linux VM.</span></span> <span data-ttu-id="3bb71-172">다음 예제는 `myVM1`이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-172">The following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="3bb71-173">두 번째 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-173">Create the second Linux VM.</span></span> <span data-ttu-id="3bb71-174">다음 예제는 `myVM2`라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-174">The following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="3bb71-175">JSON 파서를 사용하여 빌드된 모든 항목을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-175">Use the JSON parser to verify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="3bb71-176">새 환경을 템플릿으로 내보내 새 인스턴스를 빠르게 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-176">Export your new environment to a template to quickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="3bb71-177">자세한 연습</span><span class="sxs-lookup"><span data-stu-id="3bb71-177">Detailed walkthrough</span></span>
<span data-ttu-id="3bb71-178">다음에 나오는 자세한 단계는 작업 환경을 빌드할 때 각 명령이 수행하는 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-178">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="3bb71-179">이러한 개념은 개발 또는 프로덕션에 맞는 고유한 사용자 지정 환경을 빌드할 때 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="3bb71-180">[Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 로그인하여 Resource Manager 모드를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-180">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="3bb71-181">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-181">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3bb71-182">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="3bb71-183">리소스 그룹 만들기 및 배포 위치 선택</span><span class="sxs-lookup"><span data-stu-id="3bb71-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="3bb71-184">Azure 리소스 그룹은 리소스 배포를 논리적으로 관리할 수 있는 구성 정보 및 메타데이터를 포함하는 논리적 배포 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-184">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="3bb71-185">다음 예제에서는 `westeurope` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-185">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="3bb71-186">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="3bb71-187">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-187">Create a storage account</span></span>
<span data-ttu-id="3bb71-188">VM 디스크 및 추가하려는 추가 데이터 디스크에 대한 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-188">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span></span> <span data-ttu-id="3bb71-189">리소스 그룹을 만든 후 거의 즉시 저장소 계정을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="3bb71-190">여기서는 `azure storage account create` 명령을 사용하여 계정 위치, 계정을 제어할 리소스 그룹, 원하는 저장소 지원 형식을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-190">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="3bb71-191">다음 예제에서는 `mystorageaccount`라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-191">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="3bb71-192">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="3bb71-193">`azure group show` 명령을 사용하여 리소스 그룹을 검사하기 위해 `--json` Azure CLI 옵션과 함께 [jq](https://stedolan.github.io/jq/) 도구를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-193">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span></span> <span data-ttu-id="3bb71-194">( **jsawk** 또는 원하는 언어 라이브러리를 사용하여 JSON을 구문 분석할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3bb71-194">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="3bb71-195">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="3bb71-196">CLI를 사용하여 저장소 계정을 조사하려면 먼저 계정 이름과 키를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-196">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="3bb71-197">다음 예제의 저장소 계정 이름을 원하는 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-197">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="3bb71-198">그러면 저장소 정보를 쉽게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="3bb71-199">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="3bb71-200">가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="3bb71-201">다음에는 Azure에서 실행되는 가상 네트워크와 VM을 만들 수 있는 서브넷을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-201">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="3bb71-202">다음 예제는 주소 접두사 `192.168.0.0/16`으로 `myVnet`이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-202">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="3bb71-203">출력</span><span class="sxs-lookup"><span data-stu-id="3bb71-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="3bb71-204">json 옵션 `azure group show` 및 `jq`를 사용하여 리소스를 빌드하는 방법을 다시 한 번 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-204">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span></span> <span data-ttu-id="3bb71-205">이제 `storageAccounts` 리소스 및 `virtualNetworks` 리소스가 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="3bb71-206">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="3bb71-207">이번에는 VM을 배포할 `myVnet` 가상 네트워크에 서브넷을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-207">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span></span> <span data-ttu-id="3bb71-208">`azure network vnet subnet create` 명령과 이전에 만든 리소스인 `myResourceGroup` 리소스 그룹 및 `myVnet` 가상 네트워크를 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-208">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span></span> <span data-ttu-id="3bb71-209">다음 예제는 서브넷 주소 접두사 `192.168.1.0/24`로 `mySubnet`이라는 서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-209">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="3bb71-210">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up the subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up the subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="3bb71-211">서브넷은 논리적으로 가상 네트워크 안에 있으므로 약간 다른 명령을 사용하여 서브넷 정보를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-211">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span></span> <span data-ttu-id="3bb71-212">`azure network vnet show` 명령을 사용하게 되지만 `jq`를 사용하여 JSON 출력을 계속 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-212">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="3bb71-213">출력</span><span class="sxs-lookup"><span data-stu-id="3bb71-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="3bb71-214">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-214">Create a public IP address</span></span>
<span data-ttu-id="3bb71-215">이제 부하 분산 장치에 할당할 PIP(공용 IP 주소)를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-215">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="3bb71-216">이 주소가 있으면 `azure network public-ip create` 명령을 사용하여 인터넷에서 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-216">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span></span> <span data-ttu-id="3bb71-217">기본 주소는 동적이기 때문에 `--domain-name-label` 옵션을 사용하여 **cloudapp.azure.com** 도메인에 명명된 DNS 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-217">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="3bb71-218">다음 예제는 `mypublicdns`라는 DNS 이름으로 `myPublicIP`라는 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-218">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="3bb71-219">DNS 이름은 고유해야 하므로 자신만의 DNS 이름을 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb71-219">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="3bb71-220">출력</span><span class="sxs-lookup"><span data-stu-id="3bb71-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up the public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up the public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="3bb71-221">공용 IP 주소도 최상위 리소스이므로 `azure group show`를 사용하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-221">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="3bb71-222">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="3bb71-223">완전한 `azure network public-ip show` 명령을 사용하여 하위 도메인의 FQDN(정규화된 도메인 이름)을 포함하여 더 많은 리소스 세부 정보를 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-223">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span></span> <span data-ttu-id="3bb71-224">공용 IP 주소 리소스가 논리적으로 할당되었지만 아직 특정 주소가 할당되지는 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-224">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="3bb71-225">IP 주소를 획득하려면 아직 만들지 않은 부하 분산 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-225">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="3bb71-226">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="3bb71-227">부하 분산 장치 및 IP 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="3bb71-228">부하 분산 장치를 만들면 여러 VM에 트래픽을 분산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-228">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="3bb71-229">또한 유지 보수 중 또는 부하가 많을 경우 사용자 요청에 대응하는 여러 VM을 실행하여 응용 프로그램에 중복성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-229">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="3bb71-230">다음 예제는 `myLoadBalancer`라는 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-230">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="3bb71-231">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up the load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="3bb71-232">이 부하 분산 장치는 비어 있는 상태이므로 몇 개의 IP 풀을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="3bb71-233">부하 분산 장치에 프런트 엔드용과 백 엔드용으로 두 개의 IP 풀을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-233">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span></span> <span data-ttu-id="3bb71-234">프런트 엔드 IP 풀은 공개적으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-234">The front-end IP pool is publicly visible.</span></span> <span data-ttu-id="3bb71-235">이 위치에 앞에서 만든 PIP를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-235">It's also the location to which we assign the PIP that we created earlier.</span></span> <span data-ttu-id="3bb71-236">그런 후 VM을 연결할 위치로 백 엔드 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-236">Then we use the back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="3bb71-237">이런 방식으로 트래픽은 부하 분산 장치를 통해 VM에 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-237">That way, the traffic can flow through the load balancer to the VMs.</span></span>

<span data-ttu-id="3bb71-238">가장 먼저 프런트 엔드 IP 풀을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="3bb71-239">다음 예제는 `myFrontEndPool`이라는 프런트 엔드 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-239">The following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="3bb71-240">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up the load balancer "myLoadBalancer"
+ Looking up the public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="3bb71-241">앞에서 만든 `myPublicIP`를 전달하기 위해 `--public-ip-name` 스위치를 어떻게 사용했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb71-241">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="3bb71-242">부하 분산 장치에 공용 IP 주소를 할당하면 인터넷에서 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-242">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="3bb71-243">다음으로 백 엔드 트래픽에 사용할 두 번째 IP 풀을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="3bb71-244">다음 예제는 `myBackEndPool`이라는 백 엔드 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-244">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="3bb71-245">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="3bb71-246">`azure network lb show` 로 확인하고 JSON 출력을 검사하여 부하 분산 장치가 어떻게 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="3bb71-247">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="3bb71-248">부하 분산 장치 NAT 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="3bb71-249">부하 분산 장치에 트래픽을 통과시키려면 인바운드 또는 아웃바운드 동작을 지정하는 NAT(Network Address Translation) 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-249">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="3bb71-250">사용할 프로토콜을 지정한 다음 외부 포트를 내부 포트로 원하는 대로 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-250">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="3bb71-251">이 환경에서는 SSH가 이 부하 분산 장치를 통해 VM에 연결하도록 하는 몇 가지 규칙을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-251">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span></span> <span data-ttu-id="3bb71-252">TCP 포트 4222와 4223이 나중에 만들 VM의 TCP 포트 22로 연결되도록 설정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-252">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="3bb71-253">다음 예제는 TCP 포트 4222를 포트 22로 매핑하기 위해 `myLoadBalancerRuleSSH1`이라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-253">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="3bb71-254">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="3bb71-255">SSH의 두 번째 NAT 규칙에 대해 같은 절차를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-255">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="3bb71-256">다음 예제는 TCP 포트 4223을 포트 22로 매핑하기 위해 `myLoadBalancerRuleSSH2`라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-256">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="3bb71-257">또한 웹 트래픽을 위해 TCP 포트 80에 대해 NAT 규칙을 만들고 IP 풀에 규칙을 연결하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="3bb71-258">VM에 규칙을 개별적으로 연결하는 대신, IP 풀에 규칙을 연결하는 경우 IP 풀에서 VM을 추가 또는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-258">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="3bb71-259">부하 분산 장치가 자동으로 트래픽의 흐름을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-259">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="3bb71-260">다음 예제는 TCP 포트 80을 포트 80으로 매핑하기 위해 `myLoadBalancerRuleWeb`이라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-260">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="3bb71-261">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="3bb71-262">부하 분산 장치 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-262">Create a load balancer health probe</span></span>
<span data-ttu-id="3bb71-263">상태 프로브는 부하 분산 장치에 설정된 VM을 주기적으로 검사하여 VM이 정의된 대로 작동하며 요청에 응답하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-263">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="3bb71-264">그렇지 않을 경우 사용자가 오류가 발생한 VM으로 연결되지 않도록 작동을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-264">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="3bb71-265">상태 프로브에 대한 사용자 지정 검사, 간격, 시간 제한 값을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-265">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="3bb71-266">상태 프로브에 대한 자세한 내용은 [부하 분산 장치 프로브](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb71-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3bb71-267">다음 예제에는 `myHealthProbe`라는 TCP 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-267">The following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="3bb71-268">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="3bb71-269">여기서는 상태 검사 간격으로 15초를 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="3bb71-270">부하 분산 장치에서 호스트가 더 이상 작동하지 않는 것으로 판단할 때까지 최대 4개의 프로브(1분)를 놓칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-270">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

## <a name="verify-the-load-balancer"></a><span data-ttu-id="3bb71-271">부하 분산 장치 확인</span><span class="sxs-lookup"><span data-stu-id="3bb71-271">Verify the load balancer</span></span>
<span data-ttu-id="3bb71-272">이제 부하 분산 장치 구성이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-272">Now the load balancer configuration is done.</span></span> <span data-ttu-id="3bb71-273">다음과 같은 단계가 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-273">Here are the steps you took:</span></span>

1. <span data-ttu-id="3bb71-274">부하 분산 장치를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-274">You created a load balancer.</span></span>
2. <span data-ttu-id="3bb71-275">프런트 엔드 IP 풀을 만들고 공용 IP를 할당했습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-275">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="3bb71-276">VM을 연결할 수 있는 백 엔드 IP 풀을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="3bb71-277">관리를 위해 SSH가 VM에 연결할 수 있는 NAT 규칙을 만들고 웹앱이 TCP 포트 80을 사용할 수 있도록 하는 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-277">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="3bb71-278">VM을 주기적으로 확인하기 위한 상태 프로브를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-278">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="3bb71-279">이 상태 프로브는 사용자가 더 이상 작동하지 않거나 콘텐츠를 제공하지 않는 VM에 액세스하는 일이 없게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-279">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="3bb71-280">이제 부하 분산 장치가 어떻게 표시되는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="3bb71-281">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="3bb71-282">Linux VM과 함께 사용할 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-282">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="3bb71-283">NIC는 사용할 때 규칙을 적용할 수 있으므로 프로그래밍 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-283">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="3bb71-284">2개 이상 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-284">You can also have more than one.</span></span> <span data-ttu-id="3bb71-285">다음 `azure network nic create` 명령에서 NIC를 부하 백 엔드 IP 풀에 연결하고 SSH 트래픽을 허용하기 위한 NAT 규칙을 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-285">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span></span>

<span data-ttu-id="3bb71-286">`#####-###-###` 섹션을 Azure 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-286">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="3bb71-287">만드는 리소스를 검사할 때 구독 ID가 `jq` 출력에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-287">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span></span> <span data-ttu-id="3bb71-288">`azure account list`를 사용하여 구독 ID를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="3bb71-289">다음 예제는 `myNic1`이라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-289">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="3bb71-290">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up the subnet "mySubnet"
+ Looking up the network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="3bb71-291">리소스를 직접 검사하여 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-291">You can see the details by examining the resource directly.</span></span> <span data-ttu-id="3bb71-292">`azure network nic show` 명령을 사용하여 리소스를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-292">You examine the resource by using the `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="3bb71-293">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="3bb71-294">이제 두 번째 NIC를 만들고 백 엔드 IP 풀에 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-294">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="3bb71-295">이번에는 두 번째 NAT 규칙이 SSH 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-295">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="3bb71-296">다음 예제는 `myNic2`라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-296">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="3bb71-297">네트워크 보안 그룹 및 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-297">Create a network security group and rules</span></span>
<span data-ttu-id="3bb71-298">이번에는 네트워크 보안 그룹 및 NIC 액세스를 제어하는 인바운드 규칙을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-298">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="3bb71-299">네트워크 보안 그룹은 NIC 또는 서브넷에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-299">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="3bb71-300">VM 내부 및 외부로 트래픽의 흐름을 제어하도록 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-300">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="3bb71-301">다음 예제에서는 `myNetworkSecurityGroup`이라는 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-301">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="3bb71-302">포트 22에 인바운드 연결이 가능하도록(SSH를 지원하기 위해) NSG에 대한 인바운드 규칙을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-302">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="3bb71-303">다음 예제는 포트 22에서 TCP를 허용하도록 `myNetworkSecurityGroupRuleSSH`라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-303">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="3bb71-304">이제 포트 80에 인바운드 연결이 가능하도록(웹 트래픽을 지원하기 위해) NSG에 대한 인바운드 규칙을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-304">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="3bb71-305">다음 예제는 포트 80에서 TCP를 허용하도록 `myNetworkSecurityGroupRuleHTTP`라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-305">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="3bb71-306">인바운드 규칙은 인바운드 네트워크 연결에 대한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-306">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="3bb71-307">이 예제에서는 NSG를 VM 가상 NIC에 바인딩합니다. 이 경우 포트 22에 대한 모든 요청이 VM의 NIC로 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-307">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="3bb71-308">이것은 끝점이 아닌 네트워크 연결에 대한 인바운드 규칙으로, 클래식 배포와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="3bb71-309">포트를 열려면 `--source-port-range`를 '\*'(기본값)로 설정하여 **모든** 요청 포트의 인바운드 요청을 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-309">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="3bb71-310">포트는 일반적으로 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-to-the-nic"></a><span data-ttu-id="3bb71-311">NIC에 바인딩</span><span class="sxs-lookup"><span data-stu-id="3bb71-311">Bind to the NIC</span></span>
<span data-ttu-id="3bb71-312">NSG를 NIC에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-312">Bind the NSG to the NICs.</span></span> <span data-ttu-id="3bb71-313">네트워크 보안 그룹을 사용하여 NIC를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-313">We need to connect our NICs with our network security group.</span></span> <span data-ttu-id="3bb71-314">두 가지 명령을 모두 실행하여 NIC 두 개를 모두 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-314">Run both commands, to hook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="3bb71-315">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-315">Create an availability set</span></span>
<span data-ttu-id="3bb71-316">가용성 집합은 장애 도메인 및 업그레이드 도메인에 걸쳐 VM을 분산하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="3bb71-317">VM의 가용성 집합을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="3bb71-318">다음 예제는 `myAvailabilitySet`라는 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-318">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="3bb71-319">장애 도메인은 공통의 전원 및 네트워크 스위치를 공유하는 가상 컴퓨터 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="3bb71-320">기본적으로 가용성 집합 안에 구성된 가상 컴퓨터는 최대 3개의 장애 도메인에 분산되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-320">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="3bb71-321">이러한 장애 도메인 중 하나에서 발생한 하드웨어 문제가 앱을 실행 중인 모든 VM에 영향을 미치지 않는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-321">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="3bb71-322">Azure는 가용성 집합에 VM을 배치할 때 VM을 전체 장애 도메인에 자동으로 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-322">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="3bb71-323">업그레이드 도메인은 동시에 재부팅할 수 있는 가상 컴퓨터 그룹과 기본 물리적 하드웨어를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="3bb71-324">업그레이드 도메인의 재부팅 순서는 계획된 유지 보수 중 순차적으로 진행되지 않을 수 있으며, 한 번에 하나의 업그레이드만 재부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-324">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="3bb71-325">또한 Azure는 가용성 집합에 VM을 배치할 때 VM을 업그레이드 도메인에 자동으로 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="3bb71-326">[VM의 가용성 관리](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 대한 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bb71-326">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-the-linux-vms"></a><span data-ttu-id="3bb71-327">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="3bb71-327">Create the Linux VMs</span></span>
<span data-ttu-id="3bb71-328">인터넷에서 액세스 가능한 VM을 지원하기 위해 저장소 및 네트워크 리소스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-328">You've created the storage and network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="3bb71-329">이제 해당 VM을 만들고 암호 없이 SSH 키를 사용하여 VM을 보호하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="3bb71-330">이 예에서는 가장 최근의 LTS를 기반으로 Ubuntu VM을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-330">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="3bb71-331">[Azure VM 이미지 찾기](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 설명된 대로 `azure vm image list`를 사용하여 해당 이미지 정보를 찾을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3bb71-332">`azure vm image list westeurope canonical | grep LTS`명령을 사용하여 이미지는 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-332">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="3bb71-333">이 경우 `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="3bb71-334">나중에 항상 가장 최근 빌드를 가져오도록 마지막 필드에는 `latest` 를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-334">For the last field, we pass `latest` so that in the future we always get the most recent build.</span></span> <span data-ttu-id="3bb71-335">(사용하는 문자열은 `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`입니다.)</span><span class="sxs-lookup"><span data-stu-id="3bb71-335">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="3bb71-336">다음 단계는 **ssh-keygen -t rsa -b 2048**을 사용하여 Linux 또는 Mac에서 ssh rsa 공개 키 및 개인 키 쌍을 만든 경험이 있는 사용자에게 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-336">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="3bb71-337">`~/.ssh` 디렉터리에 인증서 키 쌍이 없으면 다음과 같이 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="3bb71-338">`azure vm create --generate-ssh-keys` 옵션을 사용하여 자동으로</span><span class="sxs-lookup"><span data-stu-id="3bb71-338">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="3bb71-339">[직접 만드는 명령](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 사용하여 수동으로</span><span class="sxs-lookup"><span data-stu-id="3bb71-339">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3bb71-340">또는 VM이 만들어진 후 `--admin-password` 메서드를 사용하여 SSH 연결을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-340">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="3bb71-341">이 메서드는 일반적으로 보안 수준이 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-341">This method is typically less secure.</span></span>

<span data-ttu-id="3bb71-342">`azure vm create` 명령으로 모든 리소스 및 정보를 결합하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-342">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="3bb71-343">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up the VM "myVM1"
info:    Verifying the public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account mystorageaccount
+ Looking up the availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up the NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in the NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    The storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by the parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="3bb71-344">기본 SSH 키를 사용하여 VM에 즉시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-344">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="3bb71-345">부하 분산 장치를 통과하게 되므로 적절한 포트를 지정하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-345">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="3bb71-346">(첫 번째 VM의 경우 포트 4222를 VM에 전달하도록 NAT 규칙을 설정합니다.)</span><span class="sxs-lookup"><span data-stu-id="3bb71-346">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="3bb71-347">출력</span><span class="sxs-lookup"><span data-stu-id="3bb71-347">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="3bb71-348">이제 같은 방식으로 두 번째 VM을 만드십시오.</span><span class="sxs-lookup"><span data-stu-id="3bb71-348">Go ahead and create your second VM in the same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="3bb71-349">이제 `azure vm show myResourceGroup myVM1` 명령을 사용하여 앞에서 만든 항목을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-349">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span></span> <span data-ttu-id="3bb71-350">이 시점에는 암호가 사용되지 않도록 설정되어 있으므로 Azure의 부하 분산 장치에서 Ubuntu VM을 실행 중이며 보유하고 있는 SSH 키 쌍을 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="3bb71-351">nginx 또는 httpd를 설치하고 웹앱을 배포한 다음 트래픽이 부하 분산 장치를 통해 두 VM에 연결되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-351">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="3bb71-352">출력:</span><span class="sxs-lookup"><span data-stu-id="3bb71-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "TestVM1"
+ Looking up the NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="3bb71-353">환경을 템플릿으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="3bb71-353">Export the environment as a template</span></span>
<span data-ttu-id="3bb71-354">지금까지 이 환경을 빌드했습니다. 동일한 매개 변수를 사용하여 추가 개발 환경을 만들려고 하거나 일치하는 프로덕션 환경을 만들려면 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="3bb71-354">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="3bb71-355">Resource Manager는 사용자 환경에 대한 모든 매개 변수를 정의하는 JSON 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-355">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="3bb71-356">이 JSON 템플릿을 참조하여 전체 환경을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="3bb71-357">[JSON 템플릿을 수동으로 빌드](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)하거나 기존 환경을 내보내 JSON 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="3bb71-358">이 명령을 실행하면 `myResourceGroup.json` 파일이 현재 작업 디렉터리에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-358">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="3bb71-359">그런 다음 이 템플릿에서 환경을 만들 경우 부하 분산 장치, 네트워크 인터페이스 또는 VM의 이름과 같은 모든 리소스 이름을 지정하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-359">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="3bb71-360">앞에 나온 `azure group export` 명령에 `-p` 또는 `--includeParameterDefaultValue` 매개 변수를 추가하여 템플릿 파일에 이러한 이름을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-360">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="3bb71-361">JSON 템플릿을 편집하여 리소스 이름을 지정하거나 리소스 이름을 지정하는 [parameters.json 파일을 만듭니다](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="3bb71-361">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="3bb71-362">템플릿에서 환경을 만들려면</span><span class="sxs-lookup"><span data-stu-id="3bb71-362">To create an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="3bb71-363">[템플릿에서 배포하는 방법에 대해 자세히 읽어볼 수 있습니다](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3bb71-363">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3bb71-364">환경을 점진적으로 업데이트하고, 매개 변수 파일을 사용하고, 단일 저장소 위치에서 템플릿에 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-364">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bb71-365">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3bb71-365">Next steps</span></span>
<span data-ttu-id="3bb71-366">이제 여러 네트워킹 구성 요소 및 VM을 사용할 준비가 되셨습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-366">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="3bb71-367">이 샘플 환경에 사용하여 여기에 소개된 핵심 구성 요소로 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb71-367">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
