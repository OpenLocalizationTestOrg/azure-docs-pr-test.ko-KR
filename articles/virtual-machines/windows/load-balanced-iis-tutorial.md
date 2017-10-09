---
title: "Azure Vm에서 항상 사용 가능한 응용 프로그램 빌드-aaaTutorial | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure에서 부하 분산 장치와 함께 3 개의 Windows Vm에서 항상 사용할 수 있으며 보안 응용 프로그램"
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
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="d6527-103">Azure의 Windows 가상 컴퓨터에서 부하 분산된 고가용성 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="d6527-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="d6527-104">이 자습서에서는 탄력적인 toomaintenance 이벤트를 항상 사용 가능한 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="d6527-105">hello 앱 부하 분산 장치, 가용성 집합 및 3 개의 Windows 가상 컴퓨터 (Vm)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="d6527-106">이 자습서에서 IIS를 설치,이 자습서에 사용 하 여 다른 응용 프로그램 프레임 워크 toodeploy hello 같은 고가용성 구성 요소 및 지침 사용하실 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="d6527-107">1단계 - Azure 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="d6527-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="d6527-108">toocomplete이이 자습서에서는 hello 최신 설치 되어 있는지 확인 [Azure PowerShell](/powershell/azure/overview) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="d6527-109">먼저, tooyour 로그인 AzureRmAccount 명령 hello로 Azure 구독에에서 로그인 하 고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d6527-110">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="d6527-111">다른 Azure 리소스를 만들기 전에 필요한 toocreate 인 리소스 그룹과 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="d6527-112">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westeurope` 영역:</span><span class="sxs-lookup"><span data-stu-id="d6527-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="d6527-113">2단계 - 가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="d6527-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="d6527-114">논리적 장애 및 업데이트 도메인 간에 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="d6527-115">각 논리 도메인 hello 기본 Azure 데이터 센터에서 하드웨어의 일부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="d6527-116">둘 이상의 VM을 만들 경우 Compute 및 저장소 리소스가 이러한 도메인 간에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="d6527-117">하드웨어 구성 요소에는 유지 관리 해야 하는 경우이 배포 응용 프로그램의 hello 가용성을 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="d6527-118">가용성 집합을 통해 이러한 논리적 장애 및 업데이트 도메인을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="d6527-119">[New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)을 사용하여 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="d6527-120">hello 다음 예제에서는 가용성 명명 된 집합 `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="d6527-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="d6527-121">3단계 - 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="d6527-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="d6527-122">Azure Load Balancer는 부하 분산 장치 규칙을 사용하여 정의된 VM 집합 간에 트래픽을 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="d6527-123">상태 프로브 각 VM에서 특정된 포트를 모니터링 하 고 트래픽을 tooan 배포 VM 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="d6527-124">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="d6527-124">Create public IP address</span></span>

<span data-ttu-id="d6527-125">tooaccess 앱 hello 인터넷에서 공용 IP 주소 toohello 부하 분산 장치를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="d6527-126">[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="d6527-127">hello 다음 예제에서는 공용 IP 주소를 만들고 라는 `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="d6527-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="d6527-128">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="d6527-128">Create load balancer</span></span>

<span data-ttu-id="d6527-129">[New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig)를 사용하여 프런트 엔드 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="d6527-130">hello 다음 예제에서는 프런트 엔드 IP 주소를 만들고 라는 `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="d6527-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="d6527-131">[New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig)를 사용하여 백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="d6527-132">hello 다음 예제에서는 명명 된 백 엔드 주소 풀을 `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="d6527-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="d6527-133">이제 있는 hello 부하 분산 장치를 만들 [새로 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="d6527-134">hello 다음 예제에서는 명명 된 부하 분산 장치 `myLoadBalancer` hello를 사용 하 여 `myPublicIP` 주소:</span><span class="sxs-lookup"><span data-stu-id="d6527-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="d6527-135">상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="d6527-135">Create health probe</span></span>

<span data-ttu-id="d6527-136">tooallow hello 부하 분산 장치 toomonitor hello 상태 응용 프로그램의 상태 프로브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="d6527-137">hello 상태 프로브는 동적으로 추가 하거나 Vm의 응답 toohealth 검사에 따라 hello 부하 분산 장치 순환에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="d6527-138">기본적으로 VM은 15 초 간격으로 두 개의 연속 된 실패 후 hello 부하 분산 장치 배포에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="d6527-139">[Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig)를 사용하여 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="d6527-140">hello 다음 예제에서는 명명 된 상태 프로브 `myHealthProbe` 각 VM을 모니터링 하는:</span><span class="sxs-lookup"><span data-stu-id="d6527-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="d6527-141">부하 분산 장치 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="d6527-141">Create load balancer rule</span></span>

<span data-ttu-id="d6527-142">부하 분산 장치 규칙은 사용 되는 toodefine 트래픽 분산된 toohello Vm을가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="d6527-143">[Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig)를 사용하여 부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="d6527-144">hello 다음 예제에서는 명명 된 부하 분산 장치 규칙 `myLoadBalancerRule` 포트에서 트래픽을 분산 시키고 및 `80`:</span><span class="sxs-lookup"><span data-stu-id="d6527-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="d6527-145">포함 된 hello 부하 분산 장치를 업데이트 [집합 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="d6527-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="d6527-146">4단계 - 네트워킹 구성</span><span class="sxs-lookup"><span data-stu-id="d6527-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="d6527-147">각 VM에 tooa 가상 네트워크에 연결 하는 하나 이상의 가상 네트워크 인터페이스 카드 (Nic).</span><span class="sxs-lookup"><span data-stu-id="d6527-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="d6527-148">이 가상 네트워크 toofilter 트래픽은 정의 된 액세스 규칙에 따라 보안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="d6527-149">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="d6527-149">Create virtual network</span></span>

<span data-ttu-id="d6527-150">먼저 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig)를 사용하여 서브넷을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="d6527-151">hello 다음 예제에서는 서브넷을 만듭니다. 명명 된 `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="d6527-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="d6527-152">tooprovide 네트워크 연결 tooyour Vm을 가상 네트워크를 만듭니다 [새로 AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="d6527-153">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 `myVnet` 와 `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="d6527-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="d6527-154">네트워크 보안 구성</span><span class="sxs-lookup"><span data-stu-id="d6527-154">Configure network security</span></span>

<span data-ttu-id="d6527-155">Azure NSG([네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md))는 하나 또는 여러 가상 컴퓨터에 대한 인바운드 및 아웃바운드 트래픽을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="d6527-156">네트워크 보안 그룹 규칙은 특정 포트 또는 포트 범위에 대한 네트워크 트래픽을 허용하거나 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="d6527-157">이러한 규칙에는 미리 정의된 원본에서 시작되는 트래픽만 가상 컴퓨터와 통신할 수 있도록 원본 주소 접두사가 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="d6527-158">tooallow 트래픽 tooreach 앱 웹 서버에서 네트워크 보안 그룹 규칙으로 만들 [새로 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="d6527-159">hello 다음 예제에서는 명명 된 네트워크 보안 그룹 규칙 `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="d6527-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

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

<span data-ttu-id="d6527-160">[New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="d6527-161">hello 다음 예제에서는 명명 된 NSG `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="d6527-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="d6527-162">Hello 네트워크 보안 그룹 toohello 서브넷을 추가 [집합 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="d6527-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="d6527-163">업데이트 된 가상 네트워크 hello [집합 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="d6527-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="d6527-164">가상 네트워크 인터페이스 카드 만들기</span><span class="sxs-lookup"><span data-stu-id="d6527-164">Create virtual network interface cards</span></span>

<span data-ttu-id="d6527-165">실제 VM hello 하지 않고 분산 함수 hello 가상 NIC 리소스를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="d6527-166">hello 가상 NIC 연결된 toohello 부하 분산 장치를 이며 tooa VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="d6527-167">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="d6527-168">hello 다음 예제에서는 세 개의 가상 Nic</span><span class="sxs-lookup"><span data-stu-id="d6527-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="d6527-169">(각 VM에 대 한 가상 NIC 1 개에 대해 만드는 단계를 수행 하는 hello에서 응용 프로그램):</span><span class="sxs-lookup"><span data-stu-id="d6527-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


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

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="d6527-170">5단계: 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d6527-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="d6527-171">기본 위치에 구성 요소는 모든 hello로 만들 수 있습니다 이제 항상 사용 가능한 Vm toorun 앱.</span><span class="sxs-lookup"><span data-stu-id="d6527-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="d6527-172">Hello 사용자 이름 및 암호 사용 hello 가상 컴퓨터에서 hello 관리자 계정에 필요한 가져오기 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="d6527-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="d6527-173">Hello Vm을 만들 [새로 AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [집합 AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [집합 AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [집합-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [추가 AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), 및 [새 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="d6527-174">다음 예제는 hello 세 개의 Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-174">hello following example creates three VMs:</span></span>

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

<span data-ttu-id="d6527-175">몇 분 toocreate 걸리고 모두 세 개의 Vm을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="d6527-176">hello 부하 분산 장치 상태 프로브 때 자동으로 검색 각 VM에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="d6527-177">Hello 앱이 실행 되 면 hello 부하 분산 장치 규칙 toodistribute 트래픽을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="d6527-178">Hello 앱 설치</span><span class="sxs-lookup"><span data-stu-id="d6527-178">Install hello app</span></span> 

<span data-ttu-id="d6527-179">Azure 가상 컴퓨터 확장은 응용 프로그램을 설치 및 hello 운영 체제를 구성 하는 등 tooautomate 사용 되는 가상 컴퓨터 구성 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="d6527-180">hello [Windows에 대 한 사용자 지정 스크립트 확장](./../virtual-machines-windows-extensions-customscript.md) 은 사용 되는 toorun hello 가상 컴퓨터에서 모든 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="d6527-181">hello 스크립트는 액세스할 수 있는 모든 HTTP 끝점에 Azure 저장소에에서 저장 또는 hello 사용자 지정 스크립트 확장 구성에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="d6527-182">Hello 사용자 지정 스크립트 확장을 사용할 경우 hello Azure VM 에이전트는 hello 스크립트 실행을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="d6527-183">사용 하 여 [집합 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 사용자 지정 스크립트 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="d6527-184">확장 실행 hello `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS 웹 서버:</span><span class="sxs-lookup"><span data-stu-id="d6527-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

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

### <a name="test-your-app"></a><span data-ttu-id="d6527-185">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="d6527-185">Test your app</span></span>

<span data-ttu-id="d6527-186">Hello 있는 부하 분산 장치 프로그램의 공용 IP 주소 가져오기 [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="d6527-187">hello 다음 예제에서는 가져옵니다 hello IP 주소를 `myPublicIP` 앞에서 만든:</span><span class="sxs-lookup"><span data-stu-id="d6527-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="d6527-188">Tooa 웹 브라우저에서 hello 공용 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="d6527-189">원위치에서 hello NSG 규칙을 사용 하면 hello 기본 IIS 웹 사이트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![IIS 기본 사이트](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="d6527-191">6단계 - 관리 작업</span><span class="sxs-lookup"><span data-stu-id="d6527-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="d6527-192">Hello OS 업데이트를 설치 하는 등의 응용 프로그램을 실행 하는 Vm에 tooperform 유지 관리를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="d6527-193">늘어난된 트래픽 tooyour 앱과 toodeal, tooadd 할 수 있습니다 추가 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="d6527-194">이 섹션에서는 tooremove 하거나 hello 부하 분산 장치에서 VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="d6527-195">Hello 부하 분산 장치에서 VM을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="d6527-196">Hello 네트워크 인터페이스 카드의 hello LoadBalancerBackendAddressPools 속성 다시 설정 하 여 hello 백 엔드 주소 풀에서 VM을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="d6527-197">Hello 네트워크 인터페이스 카드 가져오기 [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="d6527-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="d6527-198">Hello 네트워크 인터페이스 카드의 hello LoadBalancerBackendAddressPools 속성을 너무 설정 $null:</span><span class="sxs-lookup"><span data-stu-id="d6527-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="d6527-199">Hello 네트워크 인터페이스 카드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="d6527-200">VM toohello 부하 분산 장치 추가</span><span class="sxs-lookup"><span data-stu-id="d6527-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="d6527-201">VM 유지 관리를 수행 하거나 tooexpand 용량이 필요한 경우 추가 VM toohello 백 엔드 주소 풀의 hello 부하 분산 장치 NIC hello 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="d6527-202">Hello 부하 분산 장치 가져오기:</span><span class="sxs-lookup"><span data-stu-id="d6527-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="d6527-203">Hello 부하 분산 장치 toohello 네트워크 인터페이스 카드의 hello 백 엔드 주소 풀을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="d6527-204">Hello 네트워크 인터페이스 카드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6527-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="d6527-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6527-205">Next Steps</span></span>

<span data-ttu-id="d6527-206">샘플 – [Azure Virtual Machine PowerShell 샘플 스크립트](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d6527-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
