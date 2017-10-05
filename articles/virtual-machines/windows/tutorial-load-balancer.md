---
title: "Azure의 Windows 가상 컴퓨터 부하 분산 방법 | Microsoft Docs"
description: "Azure Load Balancer를 사용하여 3개의 Windows VM에서 고가용성 및 보안 응용 프로그램을 만드는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6738d88d5a0430abaf3855dbf97a618e4c83617f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-windows-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="1df42-103">Azure의 Windows 가상 컴퓨터 부하를 분산하여 고가용성 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1df42-103">How to load balance Windows virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="1df42-104">부하 분산은 들어오는 요청을 여러 가상 컴퓨터에 분산하여 높은 수준의 가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="1df42-105">이 자습서에서는 트래픽을 분산하고 고가용성을 제공하는 Azure Load Balancer의 여러 다른 구성 요소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="1df42-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1df42-107">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="1df42-108">부하 분산 장치 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="1df42-109">부하 분산 장치 트래픽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="1df42-110">사용자 지정 스크립트 확장을 사용하여 기본 IIS 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-110">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="1df42-111">가상 컴퓨터 만들기 및 부하 분산 장치에 연결</span><span class="sxs-lookup"><span data-stu-id="1df42-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="1df42-112">부하 분산 장치의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="1df42-112">View a load balancer in action</span></span>
> * <span data-ttu-id="1df42-113">부하 분산 장치에서 VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="1df42-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="1df42-114">이 자습서에는 Azure PowerShell 모듈 버전 3.6 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-114">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1df42-115">` Get-Module -ListAvailable AzureRM`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-115">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="1df42-116">업그레이드해야 하는 경우 [Azure PowerShell 모듈 설치](/powershell/azure/install-azurerm-ps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1df42-116">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="1df42-117">Azure Load Balancer 개요</span><span class="sxs-lookup"><span data-stu-id="1df42-117">Azure load balancer overview</span></span>
<span data-ttu-id="1df42-118">Azure Load Balancer는 들어오는 트래픽을 정상 VM 간에 분산하여 고가용성을 제공하는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="1df42-119">부하 분산 장치 상태 프로브가 각 VM에서 지정된 포트를 모니터링하고 작동하는 VM으로만 트래픽을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="1df42-120">하나 이상의 공용 IP 주소를 포함하는 프런트 엔드 IP 구성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="1df42-121">이 프런트 엔드 IP 구성을 사용하여 인터넷을 통해 부하 분산 장치 및 응용 프로그램에 액세스하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="1df42-122">가상 컴퓨터는 가상 NIC(네트워크 인터페이스 카드)를 사용하여 부하 분산 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="1df42-123">VM으로 트래픽을 분산하기 위해 백 엔드 주소 풀에 부하 분산 장치에 연결된 가상(NIC)의 주소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="1df42-124">트래픽 흐름을 제어하려면 VM에 매핑되는 특정 포트 및 프로토콜에 대해 부하 분산 장치 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="1df42-125">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-125">Create Azure load balancer</span></span>
<span data-ttu-id="1df42-126">이 섹션에서는 부하 분산 장치의 각 구성 요소를 만들고 구성하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-126">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="1df42-127">부하 분산 장치를 만들려면 먼저 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="1df42-128">다음 예제에서는 *EastUS* 위치에 *myResourceGroupLoadBalancer*라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-128">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="1df42-129">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-129">Create a public IP address</span></span>
<span data-ttu-id="1df42-130">인터넷에서 앱에 액세스하려면 부하 분산 장치에 대한 공용 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-130">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="1df42-131">[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="1df42-132">다음 예제에서는 *myResourceGroupLoadBalancer* 리소스 그룹에 *myPublicIP*라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-132">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="1df42-133">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-133">Create a load balancer</span></span>
<span data-ttu-id="1df42-134">[New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig)를 사용하여 프런트 엔드 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="1df42-135">다음 예제에서는 *myFrontEndPool*이라는 프런트 엔드 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-135">The following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="1df42-136">[New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig)를 사용하여 백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="1df42-137">다음 예제는 *myBackEndPool*이라는 백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-137">The following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="1df42-138">이제 [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)를 사용하여 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-138">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="1df42-139">다음 예제는 *myPublicIP* 주소를 사용하여 *myLoadBalancer*라는 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-139">The following example creates a load balancer named *myLoadBalancer* using the *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="1df42-140">상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-140">Create a health probe</span></span>
<span data-ttu-id="1df42-141">부하 분산 장치가 앱의 상태를 모니터링하도록 하려면 상태 프로브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-141">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="1df42-142">상태 프로브는 상태 검사에 따라 부하 분산 장치 순환에서 VM을 동적으로 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-142">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="1df42-143">기본적으로 VM은 15초 간격으로 두 번의 연속 실패 후에 부하 분산 장치 분산에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-143">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="1df42-144">앱의 프로토콜 또는 특정 상태 확인 페이지에 따라 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="1df42-145">다음 예제에서는 TCP 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-145">The following example creates a TCP probe.</span></span> <span data-ttu-id="1df42-146">좀 더 미세 조정된 상태 검사를 위해 사용자 지정 HTTP 프로브를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="1df42-147">사용자 지정 HTTP 프로브를 사용할 경우 *healthcheck.aspx*와 같은 상태 확인 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-147">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="1df42-148">부하 분산 상태가 호스트를 순환 상태를 유지하려면 프로브는 **HTTP 200 정상** 응답을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-148">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="1df42-149">TCP 상태 프로브를 만들려면 [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-149">To create a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="1df42-150">다음 예제에서는 각 VM을 모니터링하는 *myHealthProbe*라는 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-150">The following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="1df42-151">[Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer)를 사용하여 부하 분산 장치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-151">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="1df42-152">부하 분산 장치 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-152">Create a load balancer rule</span></span>
<span data-ttu-id="1df42-153">부하 분산 장치 규칙은 VM으로 트래픽이 분산되는 방법을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-153">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="1df42-154">들어오는 트래픽에 대한 프런트 엔드 IP 구성 및 트래픽을 수신할 백 엔드 IP 풀과 필요한 원본 및 대상 포트를 함께 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-154">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="1df42-155">정상 VM만 트래픽을 수신하도록 하려면 사용할 상태 프로브도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-155">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="1df42-156">[Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig)를 사용하여 부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="1df42-157">다음 예제는 *myLoadBalancerRule*이라는 부하 분산 장치 규칙을 만든 후 *80* 포트에 대한 트래픽 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-157">The following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="1df42-158">[Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer)를 사용하여 부하 분산 장치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-158">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="1df42-159">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="1df42-159">Configure virtual network</span></span>
<span data-ttu-id="1df42-160">일부 VM을 배포하고 부하 분산 장치를 테스트하려면 지원하는 가상 네트워크 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-160">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="1df42-161">가상 네트워크에 대한 자세한 내용은 [Azure Virtual Network 관리](tutorial-virtual-network.md) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1df42-161">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="1df42-162">네트워크 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-162">Create network resources</span></span>
<span data-ttu-id="1df42-163">[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="1df42-164">다음 예제에서는 *myVnet*이라는 가상 네트워크와 *mySubnet*을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-164">The following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create the virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="1df42-165">[New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)를 사용하여 네트워크 보안 그룹 규칙을 만든 다음 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="1df42-166">[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷에 네트워크 보안 그룹을 추가한 다음 [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)를 사용하여 가상 네트워크를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-166">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="1df42-167">다음 예제에서는 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹 규칙을 만들어서 *mySubnet*에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-167">The following example creates a network security group rule named *myNetworkSecurityGroup* and applies it to *mySubnet*:</span></span>

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create the network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply the network security group to a subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update the virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="1df42-168">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="1df42-169">다음 예제에서는 3개의 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-169">The following example creates three virtual NICs.</span></span> <span data-ttu-id="1df42-170">(다음 단계에서 앱에 대해 만드는 각 VM에 대해 가상 NIC 하나씩)</span><span class="sxs-lookup"><span data-stu-id="1df42-170">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="1df42-171">언제든지 추가 가상 NIC 및 VM을 만든 후 부하 분산 장치에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-171">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="1df42-172">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-172">Create virtual machines</span></span>
<span data-ttu-id="1df42-173">앱의 고가용성을 향상시키려면 VM을 가용성 집합에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-173">To improve the high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="1df42-174">[New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)을 사용하여 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="1df42-175">다음 예제는 *myAvailabilitySet*이라는 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-175">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="1df42-176">[Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential)을 사용하여 VM의 관리자 사용자 이름과 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-176">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="1df42-177">이제 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-177">Now you can create the VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="1df42-178">다음 예제에서는 3개의 가상 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-178">The following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="1df42-179">3개의 VM을 만들고 구성하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-179">It takes a few minutes to create and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="1df42-180">사용자 지정 스크립트 확장을 사용하여 IIS 설치</span><span class="sxs-lookup"><span data-stu-id="1df42-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="1df42-181">[Windows 가상 컴퓨터를 사용자 지정하는 방법](tutorial-automate-vm-deployment.md)에 대한 이전 자습서에서 Windows용 사용자 지정 스크립트 확장을 사용하여 VM 사용자 지정을 자동화하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-181">In a previous tutorial on [How to customize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with the Custom Script Extension for Windows.</span></span> <span data-ttu-id="1df42-182">동일한 접근 방법을 사용하여 VM에서 IIS를 설치하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-182">You can use the same approach to install and configure IIS on your VMs.</span></span>

<span data-ttu-id="1df42-183">[Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension)을 사용하여 사용자 지정 스크립트 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="1df42-184">확장은 `powershell Add-WindowsFeature Web-Server`를 실행하여 IIS 웹 서버를 설치한 다음 *Default.htm* 페이지를 업데이트하여 VM의 호스트 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="1df42-185">부하 분산 장치 테스트</span><span class="sxs-lookup"><span data-stu-id="1df42-185">Test load balancer</span></span>
<span data-ttu-id="1df42-186">[Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)를 사용하여 부하 분산 장치의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="1df42-187">다음 예제에서는 앞서 만든 *myPublicIP*의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-187">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="1df42-188">그런 다음 웹 브라우저에 공용 IP 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-188">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="1df42-189">다음 예제와 같이 부하 분산 장치가 트래픽을 분산한 VM의 호스트 이름을 포함하여 웹 사이트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-189">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![실행 중인 IIS 웹 사이트](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="1df42-191">앱이 실행되는 3개의 모든 VM에서 부하 분산 장치가 트래픽을 분산하는 것을 확인하기 위해 웹 브라우저를 강제로 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-191">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="1df42-192">VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="1df42-192">Add and remove VMs</span></span>
<span data-ttu-id="1df42-193">앱이 실행되는 동안 OS 업데이트와 같은 유지 관리 작업을 VM에서 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-193">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="1df42-194">앱에 대해 증가된 트래픽을 처리하기 위해 VM을 더 추가해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-194">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="1df42-195">이 섹션에서는 부하 분산 장치에서 VM을 추가 또는 제거하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-195">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="1df42-196">부하 분산 장치에서 VM 제거</span><span class="sxs-lookup"><span data-stu-id="1df42-196">Remove a VM from the load balancer</span></span>
<span data-ttu-id="1df42-197">[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface)를 사용하여 네트워크 인터페이스 카드를 가져오고 가상 NIC의 *LoadBalancerBackendAddressPools* 속성을 *$null*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set the *LoadBalancerBackendAddressPools* property of the virtual NIC to *$null*.</span></span> <span data-ttu-id="1df42-198">마지막으로 가상 NIC를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-198">Finally, update the virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="1df42-199">앱이 실행되는 나머지 2개의 VM에서 부하 분산 장치가 트래픽을 분산하는 것을 확인하기 위해 웹 브라우저를 강제로 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-199">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="1df42-200">이제 OS 업데이트 설치 또는 VM 다시 부팅을 수행 등의 유지 관리 작업을 VM에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-200">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="1df42-201">부하 분산 장치에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="1df42-201">Add a VM to the load balancer</span></span>
<span data-ttu-id="1df42-202">VM 유지 관리를 수행한 후에 또는 용량을 확장해야 하는 경우 가상 NIC의 *LoadBalancerBackendAddressPools* 속성을 [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer)에서 *BackendAddressPool*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-202">After performing VM maintenance, or if you need to expand capacity, set the *LoadBalancerBackendAddressPools* property of the virtual NIC to the *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="1df42-203">부하 분산 장치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-203">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="1df42-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1df42-204">Next steps</span></span>

<span data-ttu-id="1df42-205">이 자습서에서는 부하 분산 장치를 만들고 VM에 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-205">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="1df42-206">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1df42-207">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="1df42-208">부하 분산 장치 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="1df42-209">부하 분산 장치 트래픽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="1df42-210">사용자 지정 스크립트 확장을 사용하여 기본 IIS 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="1df42-210">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="1df42-211">가상 컴퓨터 만들기 및 부하 분산 장치에 연결</span><span class="sxs-lookup"><span data-stu-id="1df42-211">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="1df42-212">부하 분산 장치의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="1df42-212">View a load balancer in action</span></span>
> * <span data-ttu-id="1df42-213">부하 분산 장치에서 VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="1df42-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="1df42-214">VM 네트워킹을 관리하는 방법에 대해 알아보려면 다음 자습서로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1df42-214">Advance to the next tutorial to learn how to manage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1df42-215">VM 및 가상 네트워크 관리</span><span class="sxs-lookup"><span data-stu-id="1df42-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
