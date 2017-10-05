---
title: "Azure의 Linux 가상 컴퓨터 부하 분산 방법 | Microsoft Docs"
description: "Azure Load Balancer를 사용하여 3개의 Linux VM에서 고가용성 및 보안 응용 프로그램을 만드는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7b3a089d2f6386afcc46cbc4377594be0d758fc6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-linux-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="75982-103">Azure의 Linux 가상 컴퓨터 부하를 분산하여 고가용성 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="75982-103">How to load balance Linux virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="75982-104">부하 분산은 들어오는 요청을 여러 가상 컴퓨터에 분산하여 높은 수준의 가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="75982-105">이 자습서에서는 트래픽을 분산하고 고가용성을 제공하는 Azure Load Balancer의 여러 다른 구성 요소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75982-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="75982-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75982-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75982-107">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="75982-108">부하 분산 장치 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="75982-109">부하 분산 장치 트래픽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="75982-110">cloud-init를 사용하여 기본 Node.js 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-110">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="75982-111">가상 컴퓨터 만들기 및 부하 분산 장치에 연결</span><span class="sxs-lookup"><span data-stu-id="75982-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="75982-112">부하 분산 장치의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="75982-112">View a load balancer in action</span></span>
> * <span data-ttu-id="75982-113">부하 분산 장치에서 VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="75982-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="75982-114">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="75982-115">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="75982-116">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75982-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="75982-117">Azure Load Balancer 개요</span><span class="sxs-lookup"><span data-stu-id="75982-117">Azure load balancer overview</span></span>
<span data-ttu-id="75982-118">Azure Load Balancer는 들어오는 트래픽을 정상 VM 간에 분산하여 고가용성을 제공하는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="75982-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="75982-119">부하 분산 장치 상태 프로브가 각 VM에서 지정된 포트를 모니터링하고 작동하는 VM으로만 트래픽을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="75982-120">하나 이상의 공용 IP 주소를 포함하는 프런트 엔드 IP 구성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="75982-121">이 프런트 엔드 IP 구성을 사용하여 인터넷을 통해 부하 분산 장치 및 응용 프로그램에 액세스하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="75982-122">가상 컴퓨터는 가상 NIC(네트워크 인터페이스 카드)를 사용하여 부하 분산 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="75982-123">VM으로 트래픽을 분산하기 위해 백 엔드 주소 풀에 부하 분산 장치에 연결된 가상(NIC)의 주소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="75982-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="75982-124">트래픽 흐름을 제어하려면 VM에 매핑되는 특정 포트 및 프로토콜에 대해 부하 분산 장치 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>

<span data-ttu-id="75982-125">이전 자습서를 따라 [가상 컴퓨터 확장 집합을 만든 경우](tutorial-create-vmss.md) 부하 분산 장치가 생성되었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75982-125">If you followed the previous tutorial to [create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="75982-126">이러한 모든 구성 요소는 확장 집합의 일부로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-126">All these components were configured for you as part of the scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="75982-127">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-127">Create Azure load balancer</span></span>
<span data-ttu-id="75982-128">이 섹션에서는 부하 분산 장치의 각 구성 요소를 만들고 구성하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-128">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="75982-129">부하 분산 장치를 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="75982-130">다음 예제에서는 *eastus* 위치에 *myResourceGroupLoadBalancer*라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-130">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="75982-131">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-131">Create a public IP address</span></span>
<span data-ttu-id="75982-132">인터넷에서 앱에 액세스하려면 부하 분산 장치에 대한 공용 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-132">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="75982-133">[az network public-ip create](/cli/azure/network/public-ip#create)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="75982-134">다음 예제에서는 *myResourceGroupLoadBalancer* 리소스 그룹에 *myPublicIP*라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-134">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="75982-135">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-135">Create a load balancer</span></span>
<span data-ttu-id="75982-136">[az network lb create](/cli/azure/network/lb#create)를 사용하여 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="75982-137">다음 예제에서는 *myLoadBalancer*라는 부하 분산 장치를 만들고 *myPublicIP* 주소를 프런트 엔드 IP 구성에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-137">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="75982-138">상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-138">Create a health probe</span></span>
<span data-ttu-id="75982-139">부하 분산 장치가 앱의 상태를 모니터링하도록 하려면 상태 프로브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-139">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="75982-140">상태 프로브는 상태 검사에 따라 부하 분산 장치 순환에서 VM을 동적으로 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-140">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="75982-141">기본적으로 VM은 15초 간격으로 두 번의 연속 실패 후에 부하 분산 장치 분산에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="75982-141">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="75982-142">앱의 프로토콜 또는 특정 상태 확인 페이지에 따라 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="75982-143">다음 예제에서는 TCP 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-143">The following example creates a TCP probe.</span></span> <span data-ttu-id="75982-144">좀 더 미세 조정된 상태 검사를 위해 사용자 지정 HTTP 프로브를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="75982-145">사용자 지정 HTTP 프로브를 사용할 경우 *healthcheck.js*와 같은 상태 확인 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-145">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="75982-146">부하 분산 상태가 호스트를 순환 상태를 유지하려면 프로브는 **HTTP 200 정상** 응답을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-146">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="75982-147">TCP 상태 프로브를 만들려면 [az network lb probe create](/cli/azure/network/lb/probe#create)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-147">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="75982-148">다음 예제에서는 *myHealthProbe*라는 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-148">The following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="75982-149">부하 분산 장치 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-149">Create a load balancer rule</span></span>
<span data-ttu-id="75982-150">부하 분산 장치 규칙은 VM으로 트래픽이 분산되는 방법을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75982-150">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="75982-151">들어오는 트래픽에 대한 프런트 엔드 IP 구성 및 트래픽을 수신할 백 엔드 IP 풀과 필요한 원본 및 대상 포트를 함께 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-151">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="75982-152">정상 VM만 트래픽을 수신하도록 하려면 사용할 상태 프로브도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-152">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="75982-153">[az network lb rule create](/cli/azure/network/lb/rule#create)를 사용하여 부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="75982-154">다음 예제에서는 *myLoadBalancerRule*이라는 규칙을 만들고, *myHealthProbe* 상태 프로브를 사용하고, 포트 *80*에서 트래픽 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-154">The following example creates a rule named *myLoadBalancerRule*, uses the *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="75982-155">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="75982-155">Configure virtual network</span></span>
<span data-ttu-id="75982-156">일부 VM을 배포하고 부하 분산 장치를 테스트하려면 지원하는 가상 네트워크 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-156">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="75982-157">가상 네트워크에 대한 자세한 내용은 [Azure Virtual Network 관리](tutorial-virtual-network.md) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75982-157">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="75982-158">네트워크 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-158">Create network resources</span></span>
<span data-ttu-id="75982-159">[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="75982-160">다음 예제에서는 *myVnet*이라는 가상 네트워크와 *mySubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-160">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="75982-161">네트워크 보안 그룹을 추가하려면 [az network nsg create](/cli/azure/network/nsg#create)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-161">To add a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="75982-162">다음 예제에서는 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-162">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="75982-163">[az network nsg rule create](/cli/azure/network/nsg/rule#create)를 사용하여 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="75982-164">다음 예제에서는 *myNetworkSecurityGroupRule*이라는 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-164">The following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="75982-165">가상 NIC는 [az network nic create](/cli/azure/network/nic#create)를 사용하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="75982-166">다음 예제에서는 3개의 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-166">The following example creates three virtual NICs.</span></span> <span data-ttu-id="75982-167">(다음 단계에서 앱에 대해 만드는 각 VM에 대해 가상 NIC 하나씩)</span><span class="sxs-lookup"><span data-stu-id="75982-167">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="75982-168">언제든지 추가 가상 NIC 및 VM을 만든 후 부하 분산 장치에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-168">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="75982-169">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="75982-170">cloud-init 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-170">Create cloud-init config</span></span>
<span data-ttu-id="75982-171">[처음 부팅 시 Linux 가상 컴퓨터를 사용자 지정하는 방법](tutorial-automate-vm-deployment.md)에 대한 이전 자습서에서 cloud-init를 사용하여 VM 사용자 지정을 자동화하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-171">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="75982-172">동일한 cloud-init 구성 파일을 사용하여 NGINX를 설치하고 간단한 'Hello World' Node.js 앱을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-172">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="75982-173">현재 셸에서 *cloud-init.txt*라는 파일을 만들고 다음 구성을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-173">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="75982-174">예를 들어 로컬 컴퓨터에 없는 Cloud Shell에서 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-174">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="75982-175">`sensible-editor cloud-init.txt`를 입력하여 파일을 만들고 사용할 수 있는 편집기의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="75982-175">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="75982-176">전체 cloud-init 파일, 특히 첫 줄이 올바르게 복사되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-176">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="75982-177">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-177">Create virtual machines</span></span>
<span data-ttu-id="75982-178">앱의 고가용성을 향상시키려면 VM을 가용성 집합에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-178">To improve the high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="75982-179">가용성 집합에 대한 자세한 내용은 이전 [고가용성 가상 컴퓨터를 만드는 방법](tutorial-availability-sets.md) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75982-179">For more information about availability sets, see the previous [How to create highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="75982-180">[az vm availability-set create](/cli/azure/vm/availability-set#create)를 사용하여 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="75982-181">다음 예제는 *myAvailabilitySet*이라는 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75982-181">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="75982-182">이제 [az vm create](/cli/azure/vm#create)로 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-182">Now you can create the VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="75982-183">다음 예제에서는 3개의 VM을 만들고 SSH 키가 아직 없으면 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-183">The following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="75982-184">Azure CLI에서 프롬프트로 반환한 후 실행을 계속하는 백그라운드 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-184">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="75982-185">`--no-wait` 매개 변수는 모든 작업이 완료되기를 기다리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-185">The `--no-wait` parameter does not wait for all the tasks to complete.</span></span> <span data-ttu-id="75982-186">앱에 액세스하려면 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-186">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="75982-187">부하 분산 장치 상태 프로브는 각 VM에서 앱을 실행될 경우를 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-187">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="75982-188">앱이 실행되면 부하 분산 장치 규칙은 트래픽을 분산하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-188">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="75982-189">부하 분산 장치 테스트</span><span class="sxs-lookup"><span data-stu-id="75982-189">Test load balancer</span></span>
<span data-ttu-id="75982-190">[az network public-ip show](/cli/azure/network/public-ip#show)를 사용하여 부하 분산 장치의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75982-190">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="75982-191">다음 예제에서는 앞서 만든 *myPublicIP*의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75982-191">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="75982-192">그런 다음 웹 브라우저에 공용 IP 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-192">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="75982-193">부하 분산 장치가 트래픽을 분산하도록 시작하기 전에 VM이 준비하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="75982-193">Remember - it takes a few minutes the the VMs to be ready before the load balancer starts to distribute traffic to them.</span></span> <span data-ttu-id="75982-194">다음 예제와 같이 부하 분산 장치가 트래픽을 분산한 VM의 호스트 이름을 포함하여 앱이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75982-194">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Node.js 앱 실행](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="75982-196">앱이 실행되는 3개의 모든 VM에서 부하 분산 장치가 트래픽을 분산하는 것을 확인하기 위해 웹 브라우저를 강제로 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-196">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="75982-197">VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="75982-197">Add and remove VMs</span></span>
<span data-ttu-id="75982-198">앱이 실행되는 동안 OS 업데이트와 같은 유지 관리 작업을 VM에서 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-198">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="75982-199">앱에 대해 증가된 트래픽을 처리하기 위해 VM을 더 추가해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-199">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="75982-200">이 섹션에서는 부하 분산 장치에서 VM을 추가 또는 제거하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75982-200">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="75982-201">부하 분산 장치에서 VM 제거</span><span class="sxs-lookup"><span data-stu-id="75982-201">Remove a VM from the load balancer</span></span>
<span data-ttu-id="75982-202">[az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove)를 사용하여 백 엔드 주소 풀에서 VM을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-202">You can remove a VM from the backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="75982-203">다음 예제에서는 *myLoadBalancer*에서 **myVM2**용 가상 NIC를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-203">The following example removes the virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="75982-204">앱이 실행되는 나머지 2개의 VM에서 부하 분산 장치가 트래픽을 분산하는 것을 확인하기 위해 웹 브라우저를 강제로 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-204">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="75982-205">이제 OS 업데이트 설치 또는 VM 다시 부팅을 수행 등의 유지 관리 작업을 VM에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-205">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="75982-206">부하 분산 장치에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="75982-206">Add a VM to the load balancer</span></span>
<span data-ttu-id="75982-207">VM 유지 관리를 수행한 이후 또는 용량을 확장해야 할 경우 [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add)를 사용하여 백 엔드 주소 풀에 VM을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-207">After performing VM maintenance, or if you need to expand capacity, you can add a VM to the backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="75982-208">다음 예제에서는 *myLoadBalancer*에서 **myVM2**용 가상 NIC를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="75982-208">The following example adds the virtual NIC for **myVM2** to *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="75982-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75982-209">Next steps</span></span>
<span data-ttu-id="75982-210">이 자습서에서는 부하 분산 장치를 만들고 VM에 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-210">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="75982-211">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="75982-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75982-212">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="75982-213">부하 분산 장치 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="75982-214">부하 분산 장치 트래픽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="75982-215">cloud-init를 사용하여 기본 Node.js 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="75982-215">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="75982-216">가상 컴퓨터 만들기 및 부하 분산 장치에 연결</span><span class="sxs-lookup"><span data-stu-id="75982-216">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="75982-217">부하 분산 장치의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="75982-217">View a load balancer in action</span></span>
> * <span data-ttu-id="75982-218">부하 분산 장치에서 VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="75982-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="75982-219">다음 자습서에서는 Azure Virtual Network 구성 요소에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75982-219">Advance to the next tutorial to learn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75982-220">VM 및 가상 네트워크 관리</span><span class="sxs-lookup"><span data-stu-id="75982-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
