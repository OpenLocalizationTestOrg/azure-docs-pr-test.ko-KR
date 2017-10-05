---
title: "Azure VIrtual Network 및 Linux Virtual Machines | Microsoft Docs"
description: "자습서 - Azure CLI를 사용하여 Azure Virtual Network 및 Linux Virtual Machines 관리"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2366905b8160675f77cbc41ba97540af70be8c01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-the-azure-cli"></a><span data-ttu-id="ccc89-103">Azure CLI를 사용하여 Azure Virtual Network 및 Linux Virtual Machines 관리</span><span class="sxs-lookup"><span data-stu-id="ccc89-103">Manage Azure Virtual Networks and Linux Virtual Machines with the Azure CLI</span></span>

<span data-ttu-id="ccc89-104">Azure 가상 컴퓨터는 내부 및 외부 네트워크 통신에서 Azure 네트워킹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="ccc89-105">이 자습서에서는 두 개의 가상 컴퓨터를 배포하고 이러한 VM에 Azure 네트워킹을 구성하기 위해 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="ccc89-106">이 자습서의 예제에서는 VM에서 데이터베이스 백 엔드가 있는 웹 응용 프로그램을 호스팅한다고 가정하고 있지만 응용 프로그램은 이 자습서에서 배포되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-106">The examples in this tutorial assume that the VMs are hosting a web application with a database back-end, however an application is not deployed in the tutorial.</span></span> <span data-ttu-id="ccc89-107">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ccc89-108">가상 네트워크 배포</span><span class="sxs-lookup"><span data-stu-id="ccc89-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="ccc89-109">가상 네트워크 내에 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="ccc89-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="ccc89-110">서브넷에 가상 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="ccc89-110">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="ccc89-111">가상 컴퓨터 공용 IP 주소 관리</span><span class="sxs-lookup"><span data-stu-id="ccc89-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="ccc89-112">들어오는 인터넷 트래픽 보호</span><span class="sxs-lookup"><span data-stu-id="ccc89-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="ccc89-113">VM 간 트래픽 보호</span><span class="sxs-lookup"><span data-stu-id="ccc89-113">Secure VM to VM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ccc89-114">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 자습서에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ccc89-115">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="ccc89-116">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ccc89-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="ccc89-117">VM 네트워킹 개요</span><span class="sxs-lookup"><span data-stu-id="ccc89-117">VM networking overview</span></span>

<span data-ttu-id="ccc89-118">Azure 가상 네트워크를 사용하면 네트워크에서 가상 컴퓨터, 인터넷 및 다른 Azure 서비스(예: Azure SQL 데이터베이스) 간에 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-118">Azure virtual networks enable secure network connections between virtual machines, the internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="ccc89-119">가상 네트워크는 서브넷이라는 논리적 세그먼트로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="ccc89-120">서브넷은 보안 경계로서 네트워크 흐름을 제어하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-120">Subnets are used to control network flow, and as a security boundary.</span></span> <span data-ttu-id="ccc89-121">VM을 배포할 때는 일반적으로 서브넷에 연결된 가상 네트워크 인터페이스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-121">When deploying a VM, it generally includes a virtual network interface, which is attached to a subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="ccc89-122">가상 네트워크 배포</span><span class="sxs-lookup"><span data-stu-id="ccc89-122">Deploy virtual network</span></span>

<span data-ttu-id="ccc89-123">이 자습서에서는 두 개의 서브넷이 있는 단일 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="ccc89-124">서브넷 하나는 웹 응용 프로그램을 호스트하기 위한 프런트 엔드 서브넷이고 다른 하나는 데이터베이스 서버를 호스트하기 위한 백 엔드 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="ccc89-125">가상 네트워크를 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ccc89-126">다음 예제에서는 eastus 위치에 *myRGNetwork*라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-126">The following example creates a resource group named *myRGNetwork* in the eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="ccc89-127">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="ccc89-127">Create virtual network</span></span>

<span data-ttu-id="ccc89-128">[az network vnet create](/cli/azure/network/vnet#create) 명령을 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-128">Us the [az network vnet create](/cli/azure/network/vnet#create) command to create a virtual network.</span></span> <span data-ttu-id="ccc89-129">이 예제에서 네트워크의 이름은 *mvVnet*이며, 주소 접두사는 *10.0.0.0/16*으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-129">In this example, the network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="ccc89-130">또한 서브넷은 *mySubnetFrontEnd* 이름과 *10.0.1.0/24* 접두사로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="ccc89-131">이 자습서의 뒷부분에서 프런트 엔드 VM이 이 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-131">Later in this tutorial a front-end VM is connected to this subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="ccc89-132">서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="ccc89-132">Create subnet</span></span>

<span data-ttu-id="ccc89-133">[az network vnet subnet create](/cli/azure/network/vnet/subnet#create) 명령을 사용하여 가상 네트워크에 새 서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-133">A new subnet is added to the virtual network using the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="ccc89-134">이 예제에서 서브넷의 이름은 *mySubnetBackEnd*이며, 주소 접두사는 *10.0.2.0/24*로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-134">In this example, the subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="ccc89-135">이 서브넷은 모든 백 엔드 서비스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="ccc89-136">이 시점에서 네트워크가 만들어져 하나는 프론트 엔드 서비스를, 다른 하나는 백 엔드 서비스를 위한 두 개의 서브넷으로 분할되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="ccc89-137">다음 섹션에서는 가상 컴퓨터를 만들어 이 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-137">In the next section, virtual machines are created and connected to these subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="ccc89-138">공용 IP 주소 이해</span><span class="sxs-lookup"><span data-stu-id="ccc89-138">Understand public IP address</span></span>

<span data-ttu-id="ccc89-139">공용 IP 주소를 사용하면 Azure 리소스를 인터넷에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-139">A public IP address allows Azure resources to be accessible on the internet.</span></span> <span data-ttu-id="ccc89-140">자습서의 이 섹션에서는 VM을 만들어 공용 IP 주소를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-140">In this section of the tutorial, a VM is created to demonstrate how to work with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="ccc89-141">할당 방법</span><span class="sxs-lookup"><span data-stu-id="ccc89-141">Allocation method</span></span>

<span data-ttu-id="ccc89-142">공용 IP 주소는 동적 또는 정적으로 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="ccc89-143">기본적으로 공용 IP 주소는 동적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="ccc89-144">VM 할당을 취소하는 경우 동적 IP 주소도 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="ccc89-145">이 동작은 VM 할당 취소를 포함하는 모든 작업 중에 IP 주소가 변경되게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-145">This behavior causes the IP address to change during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="ccc89-146">할당 방법은 정적으로 설정할 수 있으며, 이렇게 하면 할당 취소된 상태에서도 VM에 할당된 IP 주소는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-146">The allocation method can be set to static, which ensures that the IP address remain assigned to a VM, even during a deallocated state.</span></span> <span data-ttu-id="ccc89-147">정적으로 할당된 IP 주소를 사용하는 경우 IP 주소 자체를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-147">When using a statically allocated IP address, the IP address itself cannot be specified.</span></span> <span data-ttu-id="ccc89-148">대신 사용 가능한 주소 풀에서 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="ccc89-149">동적 할당</span><span class="sxs-lookup"><span data-stu-id="ccc89-149">Dynamic allocation</span></span>

<span data-ttu-id="ccc89-150">[az vm create](/cli/azure/vm#create) 명령으로 VM을 만들 때 기본적인 공용 IP 주소 할당 방법은 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-150">When creating a VM with the [az vm create](/cli/azure/vm#create) command, the default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="ccc89-151">다음 예제에서는 동적 IP 주소로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-151">In the following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="ccc89-152">정적 할당</span><span class="sxs-lookup"><span data-stu-id="ccc89-152">Static allocation</span></span>

<span data-ttu-id="ccc89-153">[az vm create](/cli/azure/vm#create) 명령을 사용하여 가상 컴퓨터를 만들 때 `--public-ip-address-allocation static` 인수를 포함하여 정적 공용 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-153">When creating a virtual machine using the [az vm create](/cli/azure/vm#create) command, include the `--public-ip-address-allocation static` argument to assign a static public IP address.</span></span> <span data-ttu-id="ccc89-154">이 작업은 이 자습서에서 설명하지 않지만, 다음 섹션에서는 동적으로 할당된 IP 주소가 정적으로 할당된 주소로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-154">This operation is not demonstrated in this tutorial, however in the next section a dynamically allocated IP address is changed to a statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="ccc89-155">할당 방법 변경</span><span class="sxs-lookup"><span data-stu-id="ccc89-155">Change allocation method</span></span>

<span data-ttu-id="ccc89-156">IP 주소 할당 방법은 [az network public-ip update](/cli/azure/network/public-ip#update) 명령을 사용하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-156">The IP address allocation method can be changed using the [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="ccc89-157">이 예제에서는 프런트 엔드 VM의 IP 주소 할당 방법이 정적으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-157">In this example, the IP address allocation method of the front-end VM is changed to static.</span></span>

<span data-ttu-id="ccc89-158">먼저 VM을 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-158">First, deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="ccc89-159">[az network public-ip update](/cli/azure/network/public-ip#update) 명령을 사용하여 할당 방법을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-159">Use the [az network public-ip update](/cli/azure/network/public-ip#update) command to update the allocation method.</span></span> <span data-ttu-id="ccc89-160">이 경우 `--allocation-method`는 *static*으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-160">In this case, the `--allocation-method` is being set to *static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="ccc89-161">VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-161">Start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="ccc89-162">공용 IP 주소 없음</span><span class="sxs-lookup"><span data-stu-id="ccc89-162">No public IP address</span></span>

<span data-ttu-id="ccc89-163">종종 VM은 인터넷을 통해 액세스할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-163">Often, a VM does not need to be accessible over the internet.</span></span> <span data-ttu-id="ccc89-164">공용 IP 주소 없이 VM을 만들려면 `--public-ip-address ""` 인수에 빈 따옴표 묶음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-164">To create a VM without a public IP address, use the `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="ccc89-165">이 구성은 이 자습서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="ccc89-166">네트워크 트래픽 보안</span><span class="sxs-lookup"><span data-stu-id="ccc89-166">Secure network traffic</span></span>

<span data-ttu-id="ccc89-167">NSG(네트워크 보안 그룹)에는 VNet(Azure 가상 네트워크)에 연결된 리소스에 대한 네트워크 트래픽을 허용하거나 거부하는 보안 규칙 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to Azure Virtual Networks (VNet).</span></span> <span data-ttu-id="ccc89-168">NSG는 서브넷 또는 개별 네트워크 인터페이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-168">NSGs can be associated to subnets or individual network interfaces.</span></span> <span data-ttu-id="ccc89-169">NSG가 네트워크 인터페이스에 연결되면 연결된 VM만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-169">When an NSG is associated with a network interface, it applies only the associated VM.</span></span> <span data-ttu-id="ccc89-170">NSG를 서브넷에 연결하면 규칙이 서브넷에 연결된 모든 리소스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-170">When an NSG is associated to a subnet, the rules apply to all resources connected to the subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="ccc89-171">네트워크 보안 그룹 규칙</span><span class="sxs-lookup"><span data-stu-id="ccc89-171">Network security group rules</span></span>

<span data-ttu-id="ccc89-172">NSG 규칙은 트래픽이 허용되거나 거부되는 네트워킹 포트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="ccc89-173">규칙에는 원본 및 대상 IP 주소 범위가 포함될 수 있으므로 특정 시스템이나 서브넷 간의 트래픽이 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-173">The rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="ccc89-174">NSG 규칙에는 우선 순위(1-4096 사이)도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="ccc89-175">규칙은 우선 순위에 따라 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-175">Rules are evaluated in the order of priority.</span></span> <span data-ttu-id="ccc89-176">우선 순위가 100인 규칙은 우선 순위가 200인 규칙보다 먼저 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="ccc89-177">모든 NSG에는 기본 규칙 집합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="ccc89-178">기본 규칙은 삭제할 수 없지만, 가장 낮은 우선순위가 할당되기 때문에 직접 만든 규칙으로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-178">The default rules cannot be deleted, but because they are assigned the lowest priority, they can be overridden by the rules that you create.</span></span>

- <span data-ttu-id="ccc89-179">**가상 네트워크:** 가상 네트워크에서 시작하고 끝나는 트래픽은 인바운드와 아웃바운드 방향 둘 다에서 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="ccc89-180">**인터넷:** 아웃바운드 트래픽은 허용되지만 인바운드 트래픽은 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="ccc89-181">**부하 분산 장치:** Azure의 부하 분산 장치에서 VM과 역할 인스턴스의 상태를 검색할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-181">**Load balancer** - Allow Azure’s load balancer to probe the health of your VMs and role instances.</span></span> <span data-ttu-id="ccc89-182">부하 분산된 집합을 사용하지 않는 경우 이 규칙을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="ccc89-183">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ccc89-183">Create network security groups</span></span>

<span data-ttu-id="ccc89-184">네트워크 보안 그룹은 [az vm create](/cli/azure/vm#create) 명령을 사용하여 VM과 동시에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-184">A network security group can be created at the same time as a VM using the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="ccc89-185">이렇게 하면 NSG가 VM 네트워크 인터페이스와 연결되고, 모든 원본에서 포트 *22*의 트래픽을 허용하도록 NSG 규칙이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-185">When doing so, the NSG is associated with the VMs network interface and an NSG rule is auto created to allow traffic on port *22* from any source.</span></span> <span data-ttu-id="ccc89-186">이 자습서의 앞부분에서 프런트 엔드 NSG는 프런트 엔드 VM과 함께 자동으로 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-186">Earlier in this tutorial, the front-end NSG was auto-created with the front-end VM.</span></span> <span data-ttu-id="ccc89-187">22 포트에 대한 NSG 규칙도 자동으로 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="ccc89-188">경우에 따라 기본 SSH 규칙을 만들지 않아야 하거나 NSG를 서브넷에 연결해야 하는 경우와 같이 NSG를 미리 만드는 것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-188">In some cases, it may be helpful to pre-create an NSG, such as when default SSH rules should not be created, or when the NSG should be attached to a subnet.</span></span> 

<span data-ttu-id="ccc89-189">[az network nsg create](/cli/azure/network/nsg#create) 명령을 사용하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-189">Use the [az network nsg create](/cli/azure/network/nsg#create) command to create a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="ccc89-190">NSG는 네트워크 인터페이스 대신 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-190">Instead of associating the NSG to a network interface, it is associated with a subnet.</span></span> <span data-ttu-id="ccc89-191">이 구성에서 해당 서브넷에 연결되는 모든 VM에서는 NSG 규칙을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-191">In this configuration, any VM that is attached to the subnet inherits the NSG rules.</span></span>

<span data-ttu-id="ccc89-192">*mySubnetBackEnd*라는 기존 서브넷을 새 NSG로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-192">Update the existing subnet named *mySubnetBackEnd* with the new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="ccc89-193">이제 *mySubnetBackEnd*에 연결된 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-193">Now create a virtual machine, which is attached to the *mySubnetBackEnd*.</span></span> <span data-ttu-id="ccc89-194">`--nsg` 인수에는 빈 큰따옴표로 묶은 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-194">Notice that the `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="ccc89-195">VM과 함께 NSG를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-195">An NSG does not need to be created with the VM.</span></span> <span data-ttu-id="ccc89-196">VM은 미리 만든 백 엔드 NSG로 보호되는 백 엔드 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-196">The VM is attached to the back-end subnet, which is protected with the pre-created back-end NSG.</span></span> <span data-ttu-id="ccc89-197">이 NSG는 VM에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-197">This NSG applies to the VM.</span></span> <span data-ttu-id="ccc89-198">또한 `--public-ip-address` 인수에도 빈 큰따옴표로 묶은 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-198">Also, notice here that the `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="ccc89-199">이 구성은 공용 IP 주소 없이 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="ccc89-200">들어오는 트래픽 보호</span><span class="sxs-lookup"><span data-stu-id="ccc89-200">Secure incoming traffic</span></span>

<span data-ttu-id="ccc89-201">프런트 엔드 VM을 만들 때 22 포트에서 들어오는 트래픽을 허용하는 NSG 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-201">When the front-end VM was created, an NSG rule was created to allow incoming traffic on port 22.</span></span> <span data-ttu-id="ccc89-202">이 규칙은 VM에 대한 SSH 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-202">This rule allows SSH connections to the VM.</span></span> <span data-ttu-id="ccc89-203">이 예제에서 트래픽은 *80* 포트에서도 허용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="ccc89-204">이 구성을 사용하면 VM에서 웹 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-204">This configuration allows a web application to be accessed on the VM.</span></span>

<span data-ttu-id="ccc89-205">[az network nsg rule create](/cli/azure/network/nsg/rule#create) 명령을 사용하여 *80* 포트에 대한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-205">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="ccc89-206">이제 프런트 엔드 VM은 *22* 포트 및 *80* 포트에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-206">The front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="ccc89-207">다른 모든 들어오는 트래픽은 네트워크 보안 그룹에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-207">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="ccc89-208">NSG 규칙 구성을 시각화하면 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-208">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="ccc89-209">[az network rule list](/cli/azure/network/nsg/rule#list) 명령을 사용하여 NSG 규칙 구성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-209">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="ccc89-210">출력:</span><span class="sxs-lookup"><span data-stu-id="ccc89-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-to-vm-traffic"></a><span data-ttu-id="ccc89-211">VM 간 트래픽 보호</span><span class="sxs-lookup"><span data-stu-id="ccc89-211">Secure VM to VM traffic</span></span>

<span data-ttu-id="ccc89-212">네트워크 보안 그룹 규칙은 VM 간에도 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="ccc89-213">이 예제에서 프런트 엔드 VM은 *22* 및 *3306* 포트에서 백 엔드 VM과 통신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-213">For this example, the front-end VM needs to communicate with the back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="ccc89-214">이 구성을 사용하면 프런트 엔드 VM에서 SSH 연결을 허용하고, 프런트 엔드 VM의 응용 프로그램에서 백 엔드 MySQL 데이터베이스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-214">This configuration allows SSH connections from the front-end VM, and also allow an application on the front-end VM to communicate with a back-end MySQL database.</span></span> <span data-ttu-id="ccc89-215">프런트 엔드 가상 컴퓨터와 백 엔드 가상 컴퓨터 간의 다른 모든 트래픽은 차단되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-215">All other traffic should be blocked between the front-end and back-end virtual machines.</span></span>

<span data-ttu-id="ccc89-216">[az network nsg rule create](/cli/azure/network/nsg/rule#create) 명령을 사용하여 22 포트에 대한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-216">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port 22.</span></span> <span data-ttu-id="ccc89-217">`--source-address-prefix` 인수에서 *10.0.1.0/24*라는 값을 지정하고 있음에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="ccc89-217">Notice that the `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="ccc89-218">이 구성은 프런트 엔드 서브넷에서 NSG를 통해서만 트래픽이 전송되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-218">This configuration ensures that only traffic from the front-end subnet is allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="ccc89-219">이제 3306 포트에서 MySQL 트래픽에 대한 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="ccc89-220">마지막으로, NSG에는 동일한 VNet에 있는 VM 간에 모든 트래픽을 허용하는 기본 규칙이 있으므로 백 엔드 NSG에서 모든 트래픽을 차단하는 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-220">Finally, because NSGs have a default rule allowing all traffic between VMs in the same VNet, a rule can be created for the back-end NSGs to block all traffic.</span></span> <span data-ttu-id="ccc89-221">`--priority`에는 *300*이라는 값이 지정되며, 이 값은 해당 NSG와 MySQL 규칙 모두에 비해 더 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-221">Notice here that the `--priority` is given a value of *300*, which is lower that both the NSG and MySQL rules.</span></span> <span data-ttu-id="ccc89-222">이 구성은 SSH 및 MySQL 트래픽이 여전히 NSG를 통해 허용되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-222">This configuration ensures that SSH and MySQL traffic is still allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="ccc89-223">이제 백 엔드 VM은 프런트 엔드 서브넷의 *22* 및 *3306*  포트에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-223">The back-end VM is now only accessible on port *22* and port *3306* from the front-end subnet.</span></span> <span data-ttu-id="ccc89-224">다른 모든 들어오는 트래픽은 네트워크 보안 그룹에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-224">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="ccc89-225">NSG 규칙 구성을 시각화하면 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-225">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="ccc89-226">[az network rule list](/cli/azure/network/nsg/rule#list) 명령을 사용하여 NSG 규칙 구성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-226">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="ccc89-227">출력:</span><span class="sxs-lookup"><span data-stu-id="ccc89-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="ccc89-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ccc89-228">Next steps</span></span>

<span data-ttu-id="ccc89-229">이 자습서에서는 가상 컴퓨터와 관련된 Azure 네트워크를 만들고 보호했습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-229">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> <span data-ttu-id="ccc89-230">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ccc89-231">가상 네트워크 배포</span><span class="sxs-lookup"><span data-stu-id="ccc89-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="ccc89-232">가상 네트워크 내에 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="ccc89-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="ccc89-233">서브넷에 가상 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="ccc89-233">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="ccc89-234">가상 컴퓨터 공용 IP 주소 관리</span><span class="sxs-lookup"><span data-stu-id="ccc89-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="ccc89-235">들어오는 인터넷 트래픽 보호</span><span class="sxs-lookup"><span data-stu-id="ccc89-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="ccc89-236">VM 간 트래픽 보호</span><span class="sxs-lookup"><span data-stu-id="ccc89-236">Secure VM to VM traffic</span></span>

<span data-ttu-id="ccc89-237">Azure 백업을 사용하여 가상 컴퓨터의 데이터 보안에 대해 알아 보려면 다음 자습서로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc89-237">Advance to the next tutorial to learn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="ccc89-238">Azure에서 Linux 가상 컴퓨터 백업</span><span class="sxs-lookup"><span data-stu-id="ccc89-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
