---
title: "aaaHow tooload 균형 Windows Azure의 가상 컴퓨터 | Microsoft Docs"
description: "Toouse hello Azure 세 개의 Windows Vm 간에 분산 toocreate 항상 사용할 수 있으며 보안 응용 프로그램을 로드 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="76c3d-103">어떻게 tooload 균형 Azure toocreate의 Windows 가상 컴퓨터는 항상 사용 가능한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="76c3d-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="76c3d-104">부하 분산은 들어오는 요청을 여러 가상 컴퓨터에 분산하여 높은 수준의 가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="76c3d-105">이 자습서에서는 hello의 여러 구성 요소가 hello Azure 부하 분산 장치 트래픽을 분산 및 고가용성을 제공 하는 방법에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="76c3d-106">다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="76c3d-107">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="76c3d-108">부하 분산 장치 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="76c3d-109">부하 분산 장치 트래픽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="76c3d-110">사용자 지정 스크립트 확장 toocreate hello 기본 IIS 사이트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="76c3d-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="76c3d-111">가상 컴퓨터를 만들고 연결 하려면 tooa 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="76c3d-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="76c3d-112">부하 분산 장치의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="76c3d-112">View a load balancer in action</span></span>
> * <span data-ttu-id="76c3d-113">부하 분산 장치에서 VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="76c3d-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="76c3d-114">이 자습서는 Azure PowerShell 모듈 버전 3.6 이상 hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="76c3d-115">실행 ` Get-Module -ListAvailable AzureRM` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="76c3d-116">Tooupgrade 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="76c3d-117">Azure Load Balancer 개요</span><span class="sxs-lookup"><span data-stu-id="76c3d-117">Azure load balancer overview</span></span>
<span data-ttu-id="76c3d-118">Azure Load Balancer는 들어오는 트래픽을 정상 VM 간에 분산하여 고가용성을 제공하는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="76c3d-119">부하 분산 장치 상태 프로브 각 VM에서 특정된 포트를 모니터링 하 고 트래픽을 tooan 배포 VM 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="76c3d-120">하나 이상의 공용 IP 주소를 포함하는 프런트 엔드 IP 구성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="76c3d-121">이 프런트 엔드 IP 구성을 사용 하면 부하 분산 장치 및 응용 프로그램 toobe 액세스할 수 있는 hello 인터넷을 통해.</span><span class="sxs-lookup"><span data-stu-id="76c3d-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="76c3d-122">가상 컴퓨터의 가상 네트워크 인터페이스 카드 (NIC)를 사용 하 여 tooa 부하 분산 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="76c3d-123">toodistribute 트래픽 toohello Vm, 백 엔드 주소 풀을 hello 가상 (Nic) 연결 된 toohello 부하 분산 장치의 hello IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="76c3d-124">트래픽 toocontrol hello 흐름을 정의한 특정 포트 및 프로토콜 tooyour Vm을 매핑하는 대 한 부하 분산 장치 규칙.</span><span class="sxs-lookup"><span data-stu-id="76c3d-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="76c3d-125">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-125">Create Azure load balancer</span></span>
<span data-ttu-id="76c3d-126">이 섹션에는 만들어 hello 부하 분산 장치의 각 구성 요소를 구성 하는 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="76c3d-127">부하 분산 장치를 만들려면 먼저 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="76c3d-128">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupLoadBalancer* hello에 *EastUS* 위치:</span><span class="sxs-lookup"><span data-stu-id="76c3d-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="76c3d-129">공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-129">Create a public IP address</span></span>
<span data-ttu-id="76c3d-130">tooaccess 앱에서 인터넷 hello hello 부하 분산 장치에 대 한 공용 IP 주소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="76c3d-131">[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)를 사용하여 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="76c3d-132">hello 다음 예제에서는 명명 된 공용 IP 주소를 *myPublicIP* hello에 *myResourceGroupLoadBalancer* 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="76c3d-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="76c3d-133">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-133">Create a load balancer</span></span>
<span data-ttu-id="76c3d-134">[New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig)를 사용하여 프런트 엔드 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="76c3d-135">hello 다음 예제에서는 프런트 엔드 IP 주소를 만들고 명명 된 *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="76c3d-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="76c3d-136">[New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig)를 사용하여 백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="76c3d-137">hello 다음 예제에서는 명명 된 백 엔드 주소 풀을 *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="76c3d-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="76c3d-138">이제 있는 hello 부하 분산 장치를 만들 [새로 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="76c3d-139">hello 다음 예제에서는 명명 된 부하 분산 장치 *myLoadBalancer* hello를 사용 하 여 *myPublicIP* 주소:</span><span class="sxs-lookup"><span data-stu-id="76c3d-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="76c3d-140">상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-140">Create a health probe</span></span>
<span data-ttu-id="76c3d-141">tooallow hello 부하 분산 장치 toomonitor hello 상태 응용 프로그램의 상태 프로브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="76c3d-142">hello 상태 프로브는 동적으로 추가 하거나 Vm의 응답 toohealth 검사에 따라 hello 부하 분산 장치 순환에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="76c3d-143">기본적으로 VM은 15 초 간격으로 두 개의 연속 된 실패 후 hello 부하 분산 장치 배포에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="76c3d-144">앱의 프로토콜 또는 특정 상태 확인 페이지에 따라 상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="76c3d-145">다음 예제는 hello TCP 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="76c3d-146">좀 더 미세 조정된 상태 검사를 위해 사용자 지정 HTTP 프로브를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="76c3d-147">사용자 지정 HTTP 검색을 사용할 경우 만들어야 hello 상태 확인 페이지와 같은 *healthcheck.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="76c3d-148">hello 프로브를 반환 해야 합니다는 **HTTP 200 OK** hello 부하 분산 장치 tookeep hello 호스트 회전에 대 한 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="76c3d-149">사용 하면 TCP 상태 프로브 toocreate [추가 AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig)합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="76c3d-150">hello 다음 예제에서는 명명 된 상태 프로브 *myHealthProbe* 각 VM을 모니터링 하는:</span><span class="sxs-lookup"><span data-stu-id="76c3d-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="76c3d-151">포함 된 hello 부하 분산 장치를 업데이트 [집합 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="76c3d-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="76c3d-152">부하 분산 장치 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-152">Create a load balancer rule</span></span>
<span data-ttu-id="76c3d-153">부하 분산 장치 규칙은 사용 되는 toodefine 트래픽 분산된 toohello Vm을가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="76c3d-154">Hello 들어오는 트래픽의 캡슐화 된 트래픽과 hello 백 엔드 IP 풀 tooreceive hello, hello 필요한 원본 및 대상 포트에 대 한 프런트 엔드 IP 구성을 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="76c3d-155">정상 Vm만 트래픽을 받도록 toomake, 또한 정의한 hello 상태 프로브 toouse 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="76c3d-156">[Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig)를 사용하여 부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="76c3d-157">hello 다음 예제에서는 명명 된 부하 분산 장치 규칙 *myLoadBalancerRule* 포트에서 트래픽을 분산 시키고 및 *80*:</span><span class="sxs-lookup"><span data-stu-id="76c3d-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

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

<span data-ttu-id="76c3d-158">포함 된 hello 부하 분산 장치를 업데이트 [집합 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="76c3d-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="76c3d-159">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="76c3d-159">Configure virtual network</span></span>
<span data-ttu-id="76c3d-160">일부 Vm을 배포 하 여 분산 장치를 테스트할 수 전에 가상 네트워크 리소스를 지 원하는 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="76c3d-161">가상 네트워크에 대 한 자세한 내용은 참조 hello [Azure 가상 네트워크 관리](tutorial-virtual-network.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="76c3d-162">네트워크 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-162">Create network resources</span></span>
<span data-ttu-id="76c3d-163">[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)를 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="76c3d-164">hello 다음 예제에서는 가상 네트워크를 만들어 명명 된 *myVnet* 와 *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="76c3d-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="76c3d-165">[New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)를 사용하여 네트워크 보안 그룹 규칙을 만든 다음 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="76c3d-166">Hello 네트워크 보안 그룹 toohello 서브넷을 추가 [집합 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) 후 hello와 가상 네트워크를 업데이트 하 고 [집합 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="76c3d-167">hello 다음 예제에서는 명명 된 네트워크 보안 그룹 규칙 *myNetworkSecurityGroup* 너무 적용*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="76c3d-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="76c3d-168">[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)를 사용하여 가상 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="76c3d-169">hello 다음 예제에서는 세 개의 가상 Nic</span><span class="sxs-lookup"><span data-stu-id="76c3d-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="76c3d-170">(각 VM에 대 한 가상 NIC 1 개에 대해 만드는 단계를 수행 하는 hello에서 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="76c3d-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="76c3d-171">언제 든 지 가상 Nic를 추가 하 고 Vm을 만들 수 있고 toohello 부하 분산 장치를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="76c3d-172">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-172">Create virtual machines</span></span>
<span data-ttu-id="76c3d-173">tooimprove hello 고가용성 응용 프로그램의 가용성 집합에 Vm을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="76c3d-174">[New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)을 사용하여 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="76c3d-175">hello 다음 예제에서는 가용성 명명 된 집합 *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="76c3d-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="76c3d-176">된 hello Vm에 대 한 관리자 사용자 이름 및 암호 설정 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="76c3d-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="76c3d-177">Hello Vm을 만들 수 이제 [새로 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="76c3d-178">다음 예제는 hello 세 개의 Vm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-178">hello following example creates three VMs:</span></span>

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

<span data-ttu-id="76c3d-179">몇 분 toocreate 걸리고 모두 세 개의 Vm을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="76c3d-180">사용자 지정 스크립트 확장을 사용하여 IIS 설치</span><span class="sxs-lookup"><span data-stu-id="76c3d-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="76c3d-181">에 대 한 이전 자습서에서 [어떻게 toocustomize Windows 가상 컴퓨터](tutorial-automate-vm-deployment.md), tooautomate VM 사용자 지정 된 사용자 지정 스크립트 확장에 대 한 Windows hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="76c3d-182">Hello를 사용할 수 있습니다 동일 tooinstall에 접근 하 고 Vm에 IIS를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="76c3d-183">사용 하 여 [집합 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 사용자 지정 스크립트 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="76c3d-184">확장 실행 hello `powershell Add-WindowsFeature Web-Server` IIS 웹 서버 및 업데이트 hello tooinstall hello *Default.htm* hello VM의 페이지 tooshow hello 호스트 이름:</span><span class="sxs-lookup"><span data-stu-id="76c3d-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

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

## <a name="test-load-balancer"></a><span data-ttu-id="76c3d-185">부하 분산 장치 테스트</span><span class="sxs-lookup"><span data-stu-id="76c3d-185">Test load balancer</span></span>
<span data-ttu-id="76c3d-186">Hello 있는 부하 분산 장치 프로그램의 공용 IP 주소 가져오기 [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="76c3d-187">hello 다음 예제에서는 가져옵니다 hello IP 주소를 *myPublicIP* 앞에서 만든:</span><span class="sxs-lookup"><span data-stu-id="76c3d-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="76c3d-188">그런 다음 tooa 웹 브라우저에서 hello 공용 IP 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="76c3d-189">hello 웹 사이트가 표시 되어, hello VM의 hello 호스트 이름을 포함 하 여 해당 hello 부하 분산 장치는 hello 다음 예제에서에서 트래픽 tooas 분산:</span><span class="sxs-lookup"><span data-stu-id="76c3d-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![실행 중인 IIS 웹 사이트](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="76c3d-191">응용 프로그램을 실행 하는 모든 세 개의 Vm에 트래픽을 분산 toosee hello에 대 한 부하 분산 장치, 있습니다 수 강제 새로 고침 웹 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="76c3d-192">VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="76c3d-192">Add and remove VMs</span></span>
<span data-ttu-id="76c3d-193">Hello OS 업데이트를 설치 하는 등의 응용 프로그램을 실행 하는 Vm에 tooperform 유지 관리를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="76c3d-194">늘어난된 트래픽 tooyour 앱과 toodeal, tooadd 할 수 있습니다 추가 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="76c3d-195">이 섹션에서는 tooremove 하거나 hello 부하 분산 장치에서 VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="76c3d-196">Hello 부하 분산 장치에서 VM을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="76c3d-197">Hello 네트워크 인터페이스 카드 가져오기 [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), 다음 집합 hello *LoadBalancerBackendAddressPools* 속성의 가상 NIC를 너무 hello*$null*합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="76c3d-198">Hello 가상 NIC.를 마지막으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="76c3d-199">나머지 두 hello에 트래픽을 분산 toosee hello에 대 한 부하 분산 장치 앱을 실행 하는 Vm 있습니다 수 강제 새로 고침 웹 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="76c3d-200">이제 hello OS 업데이트를 설치 하 여 VM 다시 부팅 수행 등 VM에 유지 관리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="76c3d-201">VM toohello 부하 분산 장치 추가</span><span class="sxs-lookup"><span data-stu-id="76c3d-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="76c3d-202">After VM 유지 관리 수행 또는 tooexpand 용량이 필요한 경우 설정 hello *LoadBalancerBackendAddressPools* hello 가상 NIC toohello 속성 *BackendAddressPool* 에서 [ Get AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="76c3d-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="76c3d-203">Hello 부하 분산 장치 가져오기:</span><span class="sxs-lookup"><span data-stu-id="76c3d-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="76c3d-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76c3d-204">Next steps</span></span>

<span data-ttu-id="76c3d-205">이 자습서에서는 부하 분산 장치 만들고 Vm tooit 첨부 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="76c3d-206">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="76c3d-207">Azure Load Balancer 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="76c3d-208">부하 분산 장치 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="76c3d-209">부하 분산 장치 트래픽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="76c3d-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="76c3d-210">사용자 지정 스크립트 확장 toocreate hello 기본 IIS 사이트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="76c3d-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="76c3d-211">가상 컴퓨터를 만들고 연결 하려면 tooa 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="76c3d-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="76c3d-212">부하 분산 장치의 실제 동작 보기</span><span class="sxs-lookup"><span data-stu-id="76c3d-212">View a load balancer in action</span></span>
> * <span data-ttu-id="76c3d-213">부하 분산 장치에서 VM 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="76c3d-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="76c3d-214">다음 자습서 toolearn toohello 어떻게 발전 toomanage VM 네트워킹 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c3d-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="76c3d-215">VM 및 가상 네트워크 관리</span><span class="sxs-lookup"><span data-stu-id="76c3d-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
