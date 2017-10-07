---
title: "Azure에서 Linux 가상 컴퓨터를 분산 하는 aaaHow tooload | Microsoft Docs"
description: "Toouse hello Azure Linux Vm의 경우 3 개 간에 분산 toocreate 항상 사용할 수 있으며 보안 응용 프로그램을 로드 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="2b4e5-103">어떻게 tooload 균형 toocreate Azure에서 Linux 가상 컴퓨터는 항상 사용 가능한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2b4e5-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="2b4e5-104">부하 분산은 들어오는 요청을 여러 가상 컴퓨터에 분산하여 높은 수준의 가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="2b4e5-105">이 자습서에서는 hello의 여러 구성 요소가 hello Azure 부하 분산 장치 트래픽을 분산 및 고가용성을 제공 하는 방법에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="2b4e5-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b4e5-107">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="2b4e5-108">부하 분산 장치 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="2b4e5-109">부하 분산 장치 트래픽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="2b4e5-110">클라우드 init toocreate 기본 Node.js 응용 프로그램을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2b4e5-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="2b4e5-111">가상 컴퓨터를 만들고 연결 하려면 tooa 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="2b4e5-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="2b4e5-112">부하 분산 장치의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-112">View a load balancer in action</span></span>
> * <span data-ttu-id="2b4e5-113">부하 분산 장치에서 VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="2b4e5-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2b4e5-114">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2b4e5-115">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2b4e5-116">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="2b4e5-117">Azure Load Balancer 개요</span><span class="sxs-lookup"><span data-stu-id="2b4e5-117">Azure load balancer overview</span></span>
<span data-ttu-id="2b4e5-118">Azure Load Balancer는 들어오는 트래픽을 정상 VM 간에 분산하여 고가용성을 제공하는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="2b4e5-119">부하 분산 장치 상태 프로브 각 VM에서 특정된 포트를 모니터링 하 고 트래픽을 tooan 배포 VM 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="2b4e5-120">하나 이상의 공용 IP 주소를 포함하는 프런트 엔드 IP 구성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="2b4e5-121">이 프런트 엔드 IP 구성을 사용 하면 부하 분산 장치 및 응용 프로그램 toobe 액세스할 수 있는 hello 인터넷을 통해.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="2b4e5-122">가상 컴퓨터의 가상 네트워크 인터페이스 카드 (NIC)를 사용 하 여 tooa 부하 분산 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="2b4e5-123">toodistribute 트래픽 toohello Vm, 백 엔드 주소 풀을 hello 가상 (Nic) 연결 된 toohello 부하 분산 장치의 hello IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="2b4e5-124">트래픽 toocontrol hello 흐름을 정의한 특정 포트 및 프로토콜 tooyour Vm을 매핑하는 대 한 부하 분산 장치 규칙.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="2b4e5-125">너무 hello 이전 자습서를 따른 경우[가상 컴퓨터 크기 집합을 만들](tutorial-create-vmss.md), 부하 분산 장치에 만들어진 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="2b4e5-126">이러한 구성 요소가 모두 hello 크기 집합의 일부로 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="2b4e5-127">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-127">Create Azure load balancer</span></span>
<span data-ttu-id="2b4e5-128">이 섹션에는 만들어 hello 부하 분산 장치의 각 구성 요소를 구성 하는 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="2b4e5-129">부하 분산 장치를 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2b4e5-130">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupLoadBalancer* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="2b4e5-131">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-131">Create a public IP address</span></span>
<span data-ttu-id="2b4e5-132">tooaccess 앱에서 인터넷 hello hello 부하 분산 장치에 대 한 공용 IP 주소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="2b4e5-133">[az network public-ip create](/cli/azure/network/public-ip#create)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="2b4e5-134">hello 다음 예제에서는 명명 된 공용 IP 주소를 *myPublicIP* hello에 *myResourceGroupLoadBalancer* 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="2b4e5-135">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-135">Create a load balancer</span></span>
<span data-ttu-id="2b4e5-136">[az network lb create](/cli/azure/network/lb#create)를 사용하여 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="2b4e5-137">hello 다음 예제에서는 명명 된 부하 분산 장치 *myLoadBalancer* 및 할당 hello *myPublicIP* 주소 toohello 프런트 엔드 IP 구성:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="2b4e5-138">상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-138">Create a health probe</span></span>
<span data-ttu-id="2b4e5-139">tooallow hello 부하 분산 장치 toomonitor hello 상태 응용 프로그램의 상태 프로브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="2b4e5-140">hello 상태 프로브는 동적으로 추가 하거나 Vm의 응답 toohealth 검사에 따라 hello 부하 분산 장치 순환에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="2b4e5-141">기본적으로 VM은 15 초 간격으로 두 개의 연속 된 실패 후 hello 부하 분산 장치 배포에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="2b4e5-142">앱의 프로토콜 또는 특정 상태 확인 페이지에 따라 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="2b4e5-143">다음 예제는 hello TCP 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="2b4e5-144">좀 더 미세 조정된 상태 검사를 위해 사용자 지정 HTTP 프로브를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="2b4e5-145">사용자 지정 HTTP 검색을 사용할 경우 만들어야 hello 상태 확인 페이지와 같은 *healthcheck.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="2b4e5-146">hello 프로브를 반환 해야 합니다는 **HTTP 200 OK** hello 부하 분산 장치 tookeep hello 호스트 회전에 대 한 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="2b4e5-147">사용 하면 TCP 상태 프로브 toocreate [az 네트워크 lb 프로브 만들기](/cli/azure/network/lb/probe#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="2b4e5-148">hello 다음 예제에서는 명명 된 상태 프로브 *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="2b4e5-149">부하 분산 장치 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-149">Create a load balancer rule</span></span>
<span data-ttu-id="2b4e5-150">부하 분산 장치 규칙은 사용 되는 toodefine 트래픽 분산된 toohello Vm을가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="2b4e5-151">Hello 들어오는 트래픽의 캡슐화 된 트래픽과 hello 백 엔드 IP 풀 tooreceive hello, hello 필요한 원본 및 대상 포트에 대 한 프런트 엔드 IP 구성을 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="2b4e5-152">정상 Vm만 트래픽을 받도록 toomake, 또한 정의한 hello 상태 프로브 toouse 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="2b4e5-153">[az network lb rule create](/cli/azure/network/lb/rule#create)를 사용하여 부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="2b4e5-154">hello 다음 규칙을 만드는 예제는 명명 된 *myLoadBalancerRule*를 사용 하 여 hello *myHealthProbe* 상태 프로브와 포트에서 트래픽을 잔액 *80*:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

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


## <a name="configure-virtual-network"></a><span data-ttu-id="2b4e5-155">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="2b4e5-155">Configure virtual network</span></span>
<span data-ttu-id="2b4e5-156">일부 Vm을 배포 하 여 분산 장치를 테스트할 수 전에 가상 네트워크 리소스를 지 원하는 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="2b4e5-157">가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크 관리](tutorial-virtual-network.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="2b4e5-158">네트워크 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-158">Create network resources</span></span>
<span data-ttu-id="2b4e5-159">[az network vnet create](/cli/azure/network/vnet#create)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="2b4e5-160">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 이라는 서브넷과 *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="2b4e5-161">사용할 네트워크 보안 그룹 tooadd [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="2b4e5-162">hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="2b4e5-163">[az network nsg rule create](/cli/azure/network/nsg/rule#create)를 사용하여 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="2b4e5-164">hello 다음 예제에서는 명명 된 네트워크 보안 그룹 규칙 *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="2b4e5-165">가상 NIC는 [az network nic create](/cli/azure/network/nic#create)를 사용하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="2b4e5-166">hello 다음 예제에서는 세 개의 가상 Nic</span><span class="sxs-lookup"><span data-stu-id="2b4e5-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="2b4e5-167">(각 VM에 대 한 가상 NIC 1 개에 대해 만드는 단계를 수행 하는 hello에서 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="2b4e5-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="2b4e5-168">언제 든 지 가상 Nic를 추가 하 고 Vm을 만들 수 있고 toohello 부하 분산 장치를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="2b4e5-169">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="2b4e5-170">cloud-init 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-170">Create cloud-init config</span></span>
<span data-ttu-id="2b4e5-171">에 대 한 이전 자습서에서 [어떻게 toocustomize Linux 가상 컴퓨터를 처음 부팅할](tutorial-automate-vm-deployment.md), 방법에 대해 배웠습니다 클라우드 init로 tooautomate VM 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="2b4e5-172">에서는 동일한 클라우드 init 구성 파일 tooinstall NGINX hello 및 간단한 ' Hello World' Node.js 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="2b4e5-173">현재 셸에서 라는 파일을 만들어 *클라우드 init.txt* 붙여넣기 hello 구성에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="2b4e5-174">예를 들어 로컬 컴퓨터에 없는 클라우드 셸 hello에 hello 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="2b4e5-175">입력 `sensible-editor cloud-init.txt` toocreate 파일 hello 및 사용할 수 있는 편집기의 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="2b4e5-176">해당 hello 전체 클라우드 init 파일을 올바르게 복사 했는지 확인, 특히 첫 번째 줄을 hello:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

### <a name="create-virtual-machines"></a><span data-ttu-id="2b4e5-177">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-177">Create virtual machines</span></span>
<span data-ttu-id="2b4e5-178">tooimprove hello 고가용성 응용 프로그램의 가용성 집합에 Vm을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="2b4e5-179">가용성 집합에 대 한 자세한 내용은 참조 hello 이전 [어떻게 toocreate 항상 사용 가능한 가상 컴퓨터](tutorial-availability-sets.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="2b4e5-180">[az vm availability-set create](/cli/azure/vm/availability-set#create)를 사용하여 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="2b4e5-181">hello 다음 예제에서는 가용성 명명 된 집합 *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="2b4e5-182">Hello Vm을 만들 수 이제 [az vm 만들기](/cli/azure/vm#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2b4e5-183">hello 다음 예제에서는 세 개의 Vm 만들고 이미 존재 하지 않는 경우에 SSH 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

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

<span data-ttu-id="2b4e5-184">Hello Azure CLI toohello 프롬프트 반환 된 후 toorun 계속 하는 백그라운드 작업 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="2b4e5-185">hello `--no-wait` 작업 toocomplete hello 모두에 대 한 매개 변수를 대기 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="2b4e5-186">다른 몇 분 hello 앱에 액세스 하려면 먼저 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="2b4e5-187">hello 부하 분산 장치 상태 프로브 때 자동으로 검색 각 VM에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="2b4e5-188">Hello 앱이 실행 되 면 hello 부하 분산 장치 규칙 toodistribute 트래픽을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="2b4e5-189">부하 분산 장치 테스트</span><span class="sxs-lookup"><span data-stu-id="2b4e5-189">Test load balancer</span></span>
<span data-ttu-id="2b4e5-190">Hello 있는 부하 분산 장치 프로그램의 공용 IP 주소 가져오기 [az 네트워크 공개 ip 표시](/cli/azure/network/public-ip#show)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="2b4e5-191">hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myPublicIP* 앞에서 만든:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="2b4e5-192">그런 다음 tooa 웹 브라우저에서 hello 공용 IP 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="2b4e5-193">기억-hello 부하 분산 장치 toodistribute 트래픽 toothem를 시작 하기 전에 몇 분 hello hello Vm toobe 준비를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="2b4e5-194">hello 앱이 표시 됩니다, 그리고 hello VM의 hello 호스트 이름을 포함 하 여 해당 hello 부하 분산 장치는 hello 다음 예제에서에서 트래픽 tooas 분산:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Node.js 앱 실행](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="2b4e5-196">응용 프로그램을 실행 하는 모든 세 개의 Vm에 트래픽을 분산 toosee hello에 대 한 부하 분산 장치, 있습니다 수 강제 새로 고침 웹 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="2b4e5-197">VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="2b4e5-197">Add and remove VMs</span></span>
<span data-ttu-id="2b4e5-198">Hello OS 업데이트를 설치 하는 등의 응용 프로그램을 실행 하는 Vm에 tooperform 유지 관리를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="2b4e5-199">늘어난된 트래픽 tooyour 앱과 toodeal, tooadd 할 수 있습니다 추가 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="2b4e5-200">이 섹션에서는 tooremove 하거나 hello 부하 분산 장치에서 VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="2b4e5-201">Hello 부하 분산 장치에서 VM을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="2b4e5-202">Hello 백 엔드 주소 풀을에서 VM을 제거할 수 있습니다 [az 네트워크 nic ip 구성 주소 풀 제거](/cli/azure/network/nic/ip-config/address-pool#remove)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="2b4e5-203">다음 예제를 제거 하는 hello hello에 대 한 가상 NIC **myVM2** 에서 *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="2b4e5-204">나머지 두 hello에 트래픽을 분산 toosee hello에 대 한 부하 분산 장치 앱을 실행 하는 Vm 있습니다 수 강제 새로 고침 웹 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="2b4e5-205">이제 hello OS 업데이트를 설치 하 여 VM 다시 부팅 수행 등 VM에 유지 관리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="2b4e5-206">VM toohello 부하 분산 장치 추가</span><span class="sxs-lookup"><span data-stu-id="2b4e5-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="2b4e5-207">VM 유지 관리를 수행한 후 tooexpand 용량이 필요한 경우 사용 하 여 VM toohello 백 엔드 주소 풀을 추가할 수 있습니다 또는 [az 네트워크 nic ip 구성 주소 풀 추가](/cli/azure/network/nic/ip-config/address-pool#add)합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="2b4e5-208">hello 다음 예제에서는 추가 hello에 대 한 가상 NIC **myVM2** 너무*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="2b4e5-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b4e5-209">Next steps</span></span>
<span data-ttu-id="2b4e5-210">이 자습서에서는 부하 분산 장치 만들고 Vm tooit 첨부 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="2b4e5-211">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b4e5-212">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="2b4e5-213">부하 분산 장치 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="2b4e5-214">부하 분산 장치 트래픽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="2b4e5-215">클라우드 init toocreate 기본 Node.js 응용 프로그램을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2b4e5-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="2b4e5-216">가상 컴퓨터를 만들고 연결 하려면 tooa 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="2b4e5-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="2b4e5-217">부하 분산 장치의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="2b4e5-217">View a load balancer in action</span></span>
> * <span data-ttu-id="2b4e5-218">부하 분산 장치에서 VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="2b4e5-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="2b4e5-219">Azure 가상 네트워크 구성 요소에 대 한 자세한 toohello 다음 자습서 toolearn를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b4e5-220">VM 및 가상 네트워크 관리</span><span class="sxs-lookup"><span data-stu-id="2b4e5-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
