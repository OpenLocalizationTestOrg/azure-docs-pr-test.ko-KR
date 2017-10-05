---
title: "IPv6를 사용하는 Azure 인터넷 연결 부하 분산 장치 만들기 - PowerShell | Microsoft Docs"
description: "PowerShell을 사용하여 리소스 관리자에 대한 IPv6를 포함한 인터넷 연결 부하 분산 장치를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: 9d3cd37d3f2912301904b0a35f6fbc978d173079
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="ad61d-104">PowerShell을 사용하여 리소스 관리자에 대한 IPv6를 포함한 인터넷 연결 부하 분산 장치 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="ad61d-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad61d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad61d-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="ad61d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ad61d-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="ad61d-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="ad61d-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="ad61d-108">Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="ad61d-109">부하 분산 장치는 부하 분산 장치 집합에 있는 클라우드 서비스 또는 가상 컴퓨터의 정상 서비스 인스턴스 간에 들어오는 트래픽을 배포하여 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="ad61d-110">Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="ad61d-111">예제 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="ad61d-111">Example deployment scenario</span></span>

<span data-ttu-id="ad61d-112">다음 다이어그램은 이 문서에서 배포된 부하 분산 솔루션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-112">The following diagram illustrates the load balancing solution being deployed in this article.</span></span>

![부하 분산 장치 시나리오](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="ad61d-114">이 시나리오에서는 다음과 같은 Azure 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="ad61d-115">IPv4 및 IPv6 공용 IP 주소를 가진 인터넷 연결 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="ad61d-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="ad61d-116">공용 VIP를 개인 끝점으로 매핑하기 위한 두 개의 부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="ad61d-116">two load balancing rules to map the public VIPs to the private endpoints</span></span>
* <span data-ttu-id="ad61d-117">두 개의 VM이 들어 있는 가용성 집합</span><span class="sxs-lookup"><span data-stu-id="ad61d-117">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="ad61d-118">2개의 가상 컴퓨터(VM)</span><span class="sxs-lookup"><span data-stu-id="ad61d-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="ad61d-119">할당된 IPv4 및 IPv6 주소를 사용하는 각 VM에 대한 가상 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="ad61d-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-the-solution-using-the-azure-powershell"></a><span data-ttu-id="ad61d-120">Azure PowerShell을 사용하여 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="ad61d-120">Deploying the solution using the Azure PowerShell</span></span>

<span data-ttu-id="ad61d-121">다음 단계에서는 PowerShell과 함께 Azure Resource Manager를 사용하여 인터넷 연결 부하 분산 장치를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="ad61d-122">Azure Resource Manager를 사용하면 각 리소스가 개별적으로 생성되고 구성된 다음, 함께 사용되어 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-122">With Azure Resource Manager, each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="ad61d-123">부하 분산 장치를 배포하려면 다음 개체를 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="ad61d-124">프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="ad61d-125">백 엔드 주소 풀 - 부하 분산 장치의 네트워크 트래픽을 받는 가상 컴퓨터에 대한 NIC(네트워크 인터페이스)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="ad61d-126">부하 분산 규칙 - 백 엔드 주소 풀에 있는 포트에 부하 분산 장치의 공용 포트를 매핑하는 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="ad61d-127">인바운드 NAT 규칙 - 백 엔드 주소 풀에 있는 특정 가상 컴퓨터에 대한 포트에 부하 분산 장치의 공용 포트를 매핑하는 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="ad61d-128">프로브 - 백 엔드 주소 풀의 가상 컴퓨터 인스턴스의 가용성을 확인하는 데 사용하는 상태 프로브를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="ad61d-129">자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad61d-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="ad61d-130">Resource Manager를 사용하도록 PowerShell 설치</span><span class="sxs-lookup"><span data-stu-id="ad61d-130">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="ad61d-131">PowerShell에 대한 Azure Resource Manager 모듈의 최신 프로덕션 버전이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-131">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="ad61d-132">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="ad61d-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="ad61d-133">메시지가 표시되면 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="ad61d-134">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-134">Check the subscriptions for the account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="ad61d-135">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-135">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="ad61d-136">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="ad61d-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="ad61d-137">프런트 엔드 IP 풀에 대한 공용 IP 주소 및 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="ad61d-137">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="ad61d-138">서브넷을 사용하는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="ad61d-139">프런트 엔드 IP 주소 풀에 대한 Azure Public IP address (PIP) 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-139">Create Azure Public IP address (PIP) resources for the front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="ad61d-140">부하 분산 장치는 FQDN에 대한 접두사로 공용 IP의 도메인 레이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-140">The load balancer uses the domain label of the public IP as prefix for its FQDN.</span></span> <span data-ttu-id="ad61d-141">이 예제에서 FQDN은 *lbnrpipv4.westus.cloudapp.azure.com*과 *lbnrpipv6.westus.cloudapp.azure.com*입니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-141">In this example, the FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="ad61d-142">프런트 엔드 IP 구성 및 백 엔드 주소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="ad61d-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="ad61d-143">사용자가 만든 공용 IP 주소를 사용하는 프런트 엔드 주소 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-143">Create front-end address configuration that uses the Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="ad61d-144">백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="ad61d-145">LB 규칙, NAT 규칙, 프로브 및 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="ad61d-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="ad61d-146">이 예제에서는 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-146">This example creates the following items:</span></span>

* <span data-ttu-id="ad61d-147">포트 443~포트 4443에서 들어오는 모든 트래픽을 변환하는 NAT 규칙</span><span class="sxs-lookup"><span data-stu-id="ad61d-147">a NAT rule to translate all incoming traffic on port 443 to port 4443</span></span>
* <span data-ttu-id="ad61d-148">포트 80~포트 80에서 들어오는 모든 트래픽을 백 엔드 풀에 있는 주소로 분산하는 부하 분산 장치 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-148">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="ad61d-149">포트 3389에서 VM에 RDP 연결을 허용하는 부하 분산 장치 규칙</span><span class="sxs-lookup"><span data-stu-id="ad61d-149">a load balancer rule to allow RDP connection to the VMs on port 3389.</span></span>
* <span data-ttu-id="ad61d-150">*HealthProbe.aspx* 라는 페이지 또는 포트 8080에 대한 상태를 확인할 프로브 규칙</span><span class="sxs-lookup"><span data-stu-id="ad61d-150">a probe rule to check the health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="ad61d-151">이러한 개체를 모두 사용하는 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="ad61d-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="ad61d-152">NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-152">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="ad61d-153">상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-153">Create a health probe.</span></span> <span data-ttu-id="ad61d-154">프로브를 구성하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-154">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="ad61d-155">HTTP 프로브</span><span class="sxs-lookup"><span data-stu-id="ad61d-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="ad61d-156">또는 TCP 프로브</span><span class="sxs-lookup"><span data-stu-id="ad61d-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="ad61d-157">이 예제의 경우 TCP 프로브를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-157">For this example, we are going to use the TCP probes.</span></span>

3. <span data-ttu-id="ad61d-158">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="ad61d-159">이전에 만든 개체를 사용하여 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-159">Create the load balancer using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-the-back-end-vms"></a><span data-ttu-id="ad61d-160">백 엔드 VM에 대한 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="ad61d-160">Create NICs for the back-end VMs</span></span>

1. <span data-ttu-id="ad61d-161">NIC를 만들어야 하는 가상 네트워크 및 가상 네트워크 서브넷을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-161">Get the Virtual Network and Virtual Network Subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="ad61d-162">VM에 대한 IP 구성 및 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-162">Create IP configurations and NICs for the VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-the-newly-created-nics"></a><span data-ttu-id="ad61d-163">가상 컴퓨터를 만들고 새로 만든 NIC를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-163">Create virtual machines and assign the newly created NICs</span></span>

<span data-ttu-id="ad61d-164">VM 만들기에 대한 자세한 내용은 [리소스 관리자 및 Azure PowerShell을 사용하여 Windows 가상 컴퓨터 만들기 및 미리 구성](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ad61d-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="ad61d-165">가용성 집합 및 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ad61d-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="ad61d-166">각 VM을 만들고 이전에 만든 NIC를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ad61d-166">Create each VM and assign the previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type the username and password of the local administrator account."

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

## <a name="next-steps"></a><span data-ttu-id="ad61d-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad61d-167">Next steps</span></span>

[<span data-ttu-id="ad61d-168">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="ad61d-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="ad61d-169">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="ad61d-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="ad61d-170">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ad61d-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
