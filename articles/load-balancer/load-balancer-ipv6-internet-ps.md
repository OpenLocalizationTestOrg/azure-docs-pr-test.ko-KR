---
title: "i p v 6-PowerShell aaaCreate Azure 인터넷 연결 부하 분산 장치 | Microsoft Docs"
description: "리소스 관리자에 대 한 PowerShell을 사용 하 여 i p v 6 분산 toocreate 인터넷 연결을 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, Azure Load Balancer, 이중 스택, 공용 IP, 기본 ipv6, 모바일, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="014ce-104">PowerShell을 사용하여 리소스 관리자에 대한 IPv6를 포함한 인터넷 연결 부하 분산 장치 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="014ce-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="014ce-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="014ce-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="014ce-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="014ce-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="014ce-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="014ce-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="014ce-108">Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="014ce-109">hello 부하 분산 장치 부하 분산 장치 집합의 가상 컴퓨터 또는 클라우드 서비스의 비정상 상태 서비스 인스턴스 간에 들어오는 트래픽을 분산 하 여 고가용성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="014ce-110">Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="014ce-111">예제 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="014ce-111">Example deployment scenario</span></span>

<span data-ttu-id="014ce-112">hello 다음 다이어그램에서는 hello 부하 분산 되 고이 문서에 배포 된 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-112">hello following diagram illustrates hello load balancing solution being deployed in this article.</span></span>

![부하 분산 장치 시나리오](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="014ce-114">이 시나리오에서는 Azure 리소스를 수행 하는 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="014ce-115">IPv4 및 IPv6 공용 IP 주소를 가진 인터넷 연결 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="014ce-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="014ce-116">두 개의 끝점을 로드 균형 조정 규칙 toomap hello 공용 Vip toohello 개인</span><span class="sxs-lookup"><span data-stu-id="014ce-116">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>
* <span data-ttu-id="014ce-117">가용성 집합 toothat hello 두 Vm이 포함</span><span class="sxs-lookup"><span data-stu-id="014ce-117">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="014ce-118">2개의 가상 컴퓨터(VM)</span><span class="sxs-lookup"><span data-stu-id="014ce-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="014ce-119">할당된 IPv4 및 IPv6 주소를 사용하는 각 VM에 대한 가상 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="014ce-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a><span data-ttu-id="014ce-120">Hello Azure PowerShell을 사용 하 여 hello 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="014ce-120">Deploying hello solution using hello Azure PowerShell</span></span>

<span data-ttu-id="014ce-121">단계를 수행 하는 hello toocreate 인터넷 연결 부하 분산 장치 Azure 리소스 관리자를 사용 하 여 PowerShell을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="014ce-122">Azure 리소스 관리자와 각 리소스를 만들 고 toocreate 리소스는 조립 다음 개별적으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-122">With Azure Resource Manager, each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="014ce-123">부하 분산 장치 toodeploy 만들고 구성한 다음 개체는 hello:</span><span class="sxs-lookup"><span data-stu-id="014ce-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="014ce-124">프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="014ce-125">백 엔드 주소 풀-hello hello 부하 분산 장치에서 가상 컴퓨터 tooreceive 네트워크 트래픽에 대 한 Nic (네트워크 인터페이스)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="014ce-126">부하 분산 규칙-hello 백 엔드 주소 풀의 부하 분산 장치 tooport hello에 공용 포트 매핑 규칙을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="014ce-127">인바운드 NAT 규칙-hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트 매핑 규칙을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="014ce-128">프로브-hello 백 엔드 주소 풀에 있는 가상 컴퓨터 인스턴스의 사용 된 검색 toocheck 가용성 상태를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="014ce-129">자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="014ce-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="014ce-130">PowerShell toouse 리소스 관리자 설정</span><span class="sxs-lookup"><span data-stu-id="014ce-130">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="014ce-131">PowerShell에 대 한 hello Azure 리소스 관리자 모듈의 최신 프로덕션 버전 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-131">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="014ce-132">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="014ce-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="014ce-133">메시지가 표시되면 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="014ce-134">Hello 계정에 대 한 hello 구독을 확인</span><span class="sxs-lookup"><span data-stu-id="014ce-134">Check hello subscriptions for hello account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="014ce-135">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-135">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="014ce-136">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="014ce-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="014ce-137">가상 네트워크 및 hello 프런트 엔드 IP 풀에 대 한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="014ce-137">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="014ce-138">서브넷을 사용하는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="014ce-139">Azure 공용 IP 주소 hello 프런트 엔드 IP 주소 풀에 대 한 (PIP) 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-139">Create Azure Public IP address (PIP) resources for hello front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="014ce-140">hello 부하 분산 장치는 해당 FQDN에 대 한 접두사로 hello 공용 IP의 도메인 레이블을 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-140">hello load balancer uses hello domain label of hello public IP as prefix for its FQDN.</span></span> <span data-ttu-id="014ce-141">이 예제에서는 hello Fqdn은 *lbnrpipv4.westus.cloudapp.azure.com* 및 *lbnrpipv6.westus.cloudapp.azure.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-141">In this example, hello FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="014ce-142">프런트 엔드 IP 구성 및 백 엔드 주소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="014ce-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="014ce-143">만든 hello 공용 IP 주소를 사용 하는 프런트 엔드 주소 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-143">Create front-end address configuration that uses hello Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="014ce-144">백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="014ce-145">LB 규칙, NAT 규칙, 프로브 및 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="014ce-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="014ce-146">이 예에서는 hello 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-146">This example creates hello following items:</span></span>

* <span data-ttu-id="014ce-147">NAT 규칙 tootranslate 포트 443 tooport 4443에 들어오는 모든 트래픽을</span><span class="sxs-lookup"><span data-stu-id="014ce-147">a NAT rule tootranslate all incoming traffic on port 443 tooport 4443</span></span>
* <span data-ttu-id="014ce-148">부하 분산 장치 규칙 toobalance hello에 포트 80 tooport 80에 들어오는 모든 트래픽을 hello 백 엔드 풀에서 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-148">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="014ce-149">부하 분산 장치 규칙 tooallow RDP 연결 toohello 포트 3389에 있는 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-149">a load balancer rule tooallow RDP connection toohello VMs on port 3389.</span></span>
* <span data-ttu-id="014ce-150">명명 된 페이지에는 프로브 규칙 toocheck hello 상태 상태 *HealthProbe.aspx* 또는 포트 8080에서 서비스</span><span class="sxs-lookup"><span data-stu-id="014ce-150">a probe rule toocheck hello health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="014ce-151">이러한 개체를 모두 사용하는 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="014ce-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="014ce-152">Hello NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-152">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="014ce-153">상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-153">Create a health probe.</span></span> <span data-ttu-id="014ce-154">두 가지 방법으로 tooconfigure는 프로브</span><span class="sxs-lookup"><span data-stu-id="014ce-154">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="014ce-155">HTTP 프로브</span><span class="sxs-lookup"><span data-stu-id="014ce-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="014ce-156">또는 TCP 프로브</span><span class="sxs-lookup"><span data-stu-id="014ce-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="014ce-157">이 예에서는 TCP 프로브 toouse hello를 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-157">For this example, we are going toouse hello TCP probes.</span></span>

3. <span data-ttu-id="014ce-158">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="014ce-159">이전에 만든 hello 개체를 사용 하 여 hello 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-159">Create hello load balancer using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a><span data-ttu-id="014ce-160">백 엔드 Vm hello에 대 한 Nic를 만들려면</span><span class="sxs-lookup"><span data-stu-id="014ce-160">Create NICs for hello back-end VMs</span></span>

1. <span data-ttu-id="014ce-161">가져오기 hello 가상 네트워크 및 가상 네트워크 서브넷의 Nic hello 이곳 toobe 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-161">Get hello Virtual Network and Virtual Network Subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="014ce-162">Hello Vm에 대 한 IP 구성 및 Nic를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-162">Create IP configurations and NICs for hello VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a><span data-ttu-id="014ce-163">가상 컴퓨터를 만들고 새로 만든 Nic hello를 할당</span><span class="sxs-lookup"><span data-stu-id="014ce-163">Create virtual machines and assign hello newly created NICs</span></span>

<span data-ttu-id="014ce-164">VM 만들기에 대한 자세한 내용은 [리소스 관리자 및 Azure PowerShell을 사용하여 Windows 가상 컴퓨터 만들기 및 미리 구성](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="014ce-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="014ce-165">가용성 집합 및 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="014ce-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="014ce-166">각 VM을 만들고 만든 hello 이전 Nic를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="014ce-166">Create each VM and assign hello previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="014ce-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="014ce-167">Next steps</span></span>

[<span data-ttu-id="014ce-168">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="014ce-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="014ce-169">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="014ce-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="014ce-170">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="014ce-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
