---
title: "자습서 - Azure VM에서 고가용성 응용 프로그램 빌드 | Microsoft Docs"
description: "Azure에서 부하 분산 장치를 사용하여 3개의 Windows VM에서 고가용성 및 보안 응용 프로그램을 만드는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: 4b8690a11ec0e711782a112622e1193c24292289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="eeb72-103">Azure의 Windows 가상 컴퓨터에서 부하 분산된 고가용성 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="eeb72-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="eeb72-104">이 자습서에서는 유지 관리 이벤트에 대해 복원력이 뛰어난 고가용성 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-104">In this tutorial, you create a highly available application that is resilient to maintenance events.</span></span> <span data-ttu-id="eeb72-105">앱은 부하 분산 장치, 가용성 집합 및 3개의 Windows VM(가상 컴퓨터)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-105">The app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="eeb72-106">이 자습서를 사용하여 동일한 고가용성 구성 요소 및 지침에 따라 다른 응용 프로그램 프레임워크를 배포할 수 있지만 이 자습서에서는 IIS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-106">This tutorial installs IIS, though you can use this tutorial to deploy a different application framework using the same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="eeb72-107">1단계 - Azure 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="eeb72-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="eeb72-108">이 자습서를 완료하려면 최신 [Azure PowerShell](/powershell/azure/overview) 모듈을 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-108">To complete this tutorial, make sure that you have installed the latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="eeb72-109">먼저 Login-AzureRmAccount 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-109">First, log in to your Azure subscription with the Login-AzureRmAccount command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="eeb72-110">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="eeb72-111">다른 Azure 리소스를 만들려면 먼저 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-111">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="eeb72-112">다음 예제에서는 `westeurope` 지역에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-112">The following example creates a resource group named `myResourceGroup` in the `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="eeb72-113">2단계 - 가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="eeb72-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="eeb72-114">논리적 장애 및 업데이트 도메인 간에 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="eeb72-115">각 논리 도메인은 기본 Azure 데이터 센터의 하드웨어 부분을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-115">Each logical domain represents a portion of hardware in the underlying Azure datacenter.</span></span> <span data-ttu-id="eeb72-116">둘 이상의 VM을 만들 경우 Compute 및 저장소 리소스가 이러한 도메인 간에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="eeb72-117">이러한 분산은 하드웨어 구성 요소의 유지 관리가 필요할 경우 앱의 가용성을 유지해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-117">This distribution maintains the availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="eeb72-118">가용성 집합을 통해 이러한 논리적 장애 및 업데이트 도메인을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="eeb72-119">[New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)을 사용하여 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="eeb72-120">다음 예제는 `myAvailabilitySet`라는 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-120">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="eeb72-121">3단계 - 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="eeb72-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="eeb72-122">Azure Load Balancer는 부하 분산 장치 규칙을 사용하여 정의된 VM 집합 간에 트래픽을 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="eeb72-123">상태 프로브가 각 VM에서 지정된 포트를 모니터링하고 작동하는 VM으로만 트래픽을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-123">A health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="eeb72-124">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="eeb72-124">Create public IP address</span></span>

<span data-ttu-id="eeb72-125">인터넷에서 앱에 액세스하려면 공용 IP 주소를 부하 분산 장치에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-125">To access your app on the Internet, assign a public IP address to the load balancer.</span></span> <span data-ttu-id="eeb72-126">[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="eeb72-127">다음 예제에서는 `myPublicIP`라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-127">The following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="eeb72-128">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="eeb72-128">Create load balancer</span></span>

<span data-ttu-id="eeb72-129">[New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig)를 사용하여 프런트 엔드 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="eeb72-130">다음 예제에서는 `myFrontEndPool`라는 프런트 엔드 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-130">The following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="eeb72-131">[New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig)를 사용하여 백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="eeb72-132">다음 예제는 `myBackEndPool`이라는 백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-132">The following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="eeb72-133">이제 [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)를 사용하여 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-133">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="eeb72-134">다음 예제는 `myPublicIP` 주소를 사용하여 `myLoadBalancer`라는 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-134">The following example creates a load balancer named `myLoadBalancer` using the `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="eeb72-135">상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="eeb72-135">Create health probe</span></span>

<span data-ttu-id="eeb72-136">부하 분산 장치가 앱의 상태를 모니터링하도록 하려면 상태 프로브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-136">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="eeb72-137">상태 프로브는 상태 검사에 따라 부하 분산 장치 순환에서 VM을 동적으로 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-137">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="eeb72-138">기본적으로 VM은 15초 간격으로 두 번의 연속 실패 후에 부하 분산 장치 분산에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-138">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="eeb72-139">[Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig)를 사용하여 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="eeb72-140">다음 예제에서는 각 VM을 모니터링하는 `myHealthProbe`라는 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-140">The following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="eeb72-141">부하 분산 장치 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="eeb72-141">Create load balancer rule</span></span>

<span data-ttu-id="eeb72-142">부하 분산 장치 규칙은 VM으로 트래픽이 분산되는 방법을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-142">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span>

<span data-ttu-id="eeb72-143">[Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig)를 사용하여 부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="eeb72-144">다음 예제는 `myLoadBalancerRule`이라는 부하 분산 장치 규칙을 만든 후 `80` 포트에 대한 트래픽 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-144">The following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="eeb72-145">[Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer)를 사용하여 부하 분산 장치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-145">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="eeb72-146">4단계 - 네트워킹 구성</span><span class="sxs-lookup"><span data-stu-id="eeb72-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="eeb72-147">각 VM에는 가상 네트워크에 연결되는 하나 이상의 가상 NIC(네트워크 인터페이스 카드)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-147">Each VM has one or more virtual network interface cards (NICs) that connect to a virtual network.</span></span> <span data-ttu-id="eeb72-148">이 가상 네트워크는 정의된 액세스 규칙에 따라 트래픽을 필터링함으로써 보안이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-148">This virtual network is secured to filter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="eeb72-149">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="eeb72-149">Create virtual network</span></span>

<span data-ttu-id="eeb72-150">먼저 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="eeb72-151">다음 예제는 `mySubnet`이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-151">The following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="eeb72-152">VM에 네트워크 연결을 제공하려면 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-152">To provide network connectivity to your VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="eeb72-153">다음 예제는 `mySubnet`를 사용하여 `myVnet`이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-153">The following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="eeb72-154">네트워크 보안 구성</span><span class="sxs-lookup"><span data-stu-id="eeb72-154">Configure network security</span></span>

<span data-ttu-id="eeb72-155">Azure NSG([네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md))는 하나 또는 여러 가상 컴퓨터에 대한 인바운드 및 아웃바운드 트래픽을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="eeb72-156">네트워크 보안 그룹 규칙은 특정 포트 또는 포트 범위에 대한 네트워크 트래픽을 허용하거나 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="eeb72-157">이러한 규칙에는 미리 정의된 원본에서 시작되는 트래픽만 가상 컴퓨터와 통신할 수 있도록 원본 주소 접두사가 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="eeb72-158">웹 트래픽이 앱에 도달하게 하려면 [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)를 사용하여 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-158">To allow web traffic to reach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="eeb72-159">다음 예제에서는 `myNetworkSecurityGroupRule`이라는 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-159">The following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
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
```

<span data-ttu-id="eeb72-160">[New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="eeb72-161">다음 예제는 `myNetworkSecurityGroup`이라는 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-161">The following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="eeb72-162">[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)를 사용하여 네트워크 보안 그룹을 서브넷에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-162">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="eeb72-163">[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)를 사용하여 가상 네트워크를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-163">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="eeb72-164">가상 네트워크 인터페이스 카드 만들기</span><span class="sxs-lookup"><span data-stu-id="eeb72-164">Create virtual network interface cards</span></span>

<span data-ttu-id="eeb72-165">부하 분산 장치는 실제 VM보다는 가상 NIC 리소스에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-165">Load balancers function with the virtual NIC resource rather than the actual VM.</span></span> <span data-ttu-id="eeb72-166">가상 NIC는 부하 분산 장치에 연결된 후 VM에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-166">The virtual NIC is connected to the load balancer, and then attached to a VM.</span></span>

<span data-ttu-id="eeb72-167">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="eeb72-168">다음 예제에서는 3개의 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-168">The following example creates three virtual NICs.</span></span> <span data-ttu-id="eeb72-169">(다음 단계에서는 앱에 대한 가상 NIC를 각 VM에 대해 하나씩 만듭니다.)</span><span class="sxs-lookup"><span data-stu-id="eeb72-169">(One virtual NIC for each VM you create for your app in the following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="eeb72-170">5단계: 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="eeb72-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="eeb72-171">모든 기본 구성 요소가 구축되면 이제 앱을 실행하기 위한 고가용성 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-171">With all the underlying components in place, you can now create highly available VMs to run your app.</span></span> 

<span data-ttu-id="eeb72-172">[Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential)를 사용하여 가상 컴퓨터의 관리자 계정에 대한 사용자 이름 및 암호를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-172">Get the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="eeb72-173">[New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface) 및 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-173">Create the VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="eeb72-174">다음 예제에서는 3개의 가상 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-174">The following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="eeb72-175">3개의 VM을 모두 만들고 구성하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-175">It takes several minutes to create and configure all three VMs.</span></span> <span data-ttu-id="eeb72-176">부하 분산 장치 상태 프로브는 각 VM에서 앱을 실행될 경우를 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-176">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="eeb72-177">앱이 실행되면 부하 분산 장치 규칙은 트래픽을 분산하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-177">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>

### <a name="install-the-app"></a><span data-ttu-id="eeb72-178">앱 설치</span><span class="sxs-lookup"><span data-stu-id="eeb72-178">Install the app</span></span> 

<span data-ttu-id="eeb72-179">Azure 가상 컴퓨터 확장은 응용 프로그램 설치 및 운영 체제 구성 등 가장 컴퓨터 구성 작업을 자동화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-179">Azure virtual machine extensions are used to automate virtual machine configuration tasks such as installing applications and configuring the operating system.</span></span> <span data-ttu-id="eeb72-180">[Windows용 사용자 지정 스크립트 확장](./../virtual-machines-windows-extensions-customscript.md)은 가상 컴퓨터에서 PowerShell 스크립트를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-180">The [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used to run any PowerShell script on the virtual machine.</span></span> <span data-ttu-id="eeb72-181">스크립트를 Azure Storage, 액세스 가능한 HTTP 끝점에 저장하거나 사용자 지정 스크립트 확장 구성에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-181">The script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in the custom script extension configuration.</span></span> <span data-ttu-id="eeb72-182">사용자 지정 스크립트 확장을 사용하는 경우 Azure VM 에이전트가 스크립트 실행을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-182">When using the custom script extension, the Azure VM agent manages the script execution.</span></span>

<span data-ttu-id="eeb72-183">[Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension)을 사용하여 사용자 지정 스크립트 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the custom script extension.</span></span> <span data-ttu-id="eeb72-184">이 확장이 `powershell Add-WindowsFeature Web-Server`을 실행하여 IIS 웹 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="eeb72-185">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="eeb72-185">Test your app</span></span>

<span data-ttu-id="eeb72-186">[Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)를 사용하여 부하 분산 장치의 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="eeb72-187">다음 예제에서는 앞서 만든 `myPublicIP`의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-187">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="eeb72-188">웹 브라우저에 공용 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-188">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="eeb72-189">NSG 규칙이 설정되면 기본 IIS 웹 사이트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-189">With the NSG rule in place, the default IIS website is displayed.</span></span> 

![IIS 기본 사이트](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="eeb72-191">6단계 - 관리 작업</span><span class="sxs-lookup"><span data-stu-id="eeb72-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="eeb72-192">앱이 실행되는 동안 OS 업데이트와 같은 유지 관리 작업을 VM에서 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-192">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="eeb72-193">앱에 대해 증가된 트래픽을 처리하기 위해 VM을 더 추가해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-193">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="eeb72-194">이 섹션에서는 부하 분산 장치에서 VM을 추가 또는 제거하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-194">This section shows you how to remove or add a VM from the load balancer.</span></span> 

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="eeb72-195">부하 분산 장치에서 VM 제거</span><span class="sxs-lookup"><span data-stu-id="eeb72-195">Remove a VM from the load balancer</span></span>

<span data-ttu-id="eeb72-196">네트워크 인터페이스 카드의 LoadBalancerBackendAddressPools 속성을 재설정하여 백 엔드 주소 풀에서 VM을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-196">Remove a VM from the backend address pool by resetting the LoadBalancerBackendAddressPools property of the network interface card.</span></span>

<span data-ttu-id="eeb72-197">[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface)를 사용하여 네트워크 인터페이스 카드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="eeb72-198">네트워크 인터페이스 카드의 LoadBalancerBackendAddressPools 속성을 $null로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-198">Set the LoadBalancerBackendAddressPools property of the network interface card to $null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="eeb72-199">네트워크 인터페이스 카드 업데이트:</span><span class="sxs-lookup"><span data-stu-id="eeb72-199">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="eeb72-200">부하 분산 장치에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="eeb72-200">Add a VM to the load balancer</span></span>

<span data-ttu-id="eeb72-201">VM 유지 관리를 수행한 이후 또는 용량을 확장해야 할 경우 VM의 NIC를 부하 분산 장치의 백 엔드 주소 풀에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-201">After performing VM maintenance, or if you need to expand capacity, adding the NIC of a VM to the backend address pool of the load balancer.</span></span>

<span data-ttu-id="eeb72-202">부하 분산 장치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-202">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="eeb72-203">부하 분산 장치의 백 엔드 주소 풀을 네트워크 인터페이스 카드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb72-203">Add the backend address pool of the load balancer to the network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="eeb72-204">네트워크 인터페이스 카드 업데이트:</span><span class="sxs-lookup"><span data-stu-id="eeb72-204">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="eeb72-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eeb72-205">Next Steps</span></span>

<span data-ttu-id="eeb72-206">샘플 – [Azure Virtual Machine PowerShell 샘플 스크립트](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="eeb72-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
