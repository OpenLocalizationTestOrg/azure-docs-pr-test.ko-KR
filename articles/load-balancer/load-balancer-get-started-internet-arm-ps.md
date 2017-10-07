---
title: "aaaCreate Azure 인터넷 연결 부하 분산 장치-PowerShell | Microsoft Docs"
description: "어떻게 toocreate 인터넷 연결 부하 분산 장치 리소스 관리자의 PowerShell을 사용 하 여 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="22cd0-103"><a name="get-started"></a>PowerShell을 사용하여 Resource Manager에서 인터넷 연결 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="22cd0-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="22cd0-104">포털</span><span class="sxs-lookup"><span data-stu-id="22cd0-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="22cd0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22cd0-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="22cd0-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="22cd0-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="22cd0-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="22cd0-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="22cd0-108">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="22cd0-109">수도 있습니다 [어떻게 toocreate 인터넷 연결 부하 분산 장치 hello 클래식 배포 모델을 사용 하 여 자세한](load-balancer-get-started-internet-classic-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-109">You can also [learn how toocreate an Internet-facing load balancer by using hello classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a><span data-ttu-id="22cd0-110">Azure PowerShell을 사용 하 여 hello 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="22cd0-110">Deploying hello solution by using Azure PowerShell</span></span>

<span data-ttu-id="22cd0-111">다음 절차를 수행 하는 hello toocreate 인터넷 연결 PowerShell과 함께 Azure 리소스 관리자를 사용 하 여 분산 장치를 로드 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-111">hello following procedures explain how toocreate an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="22cd0-112">Azure 리소스 관리자와 각 리소스 만들어집니다 및 개별적으로 구성 된 한 다음 함께 toocreate 부하 분산 장치.</span><span class="sxs-lookup"><span data-stu-id="22cd0-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a load balancer.</span></span>

<span data-ttu-id="22cd0-113">만들고 해야 개체 toodeploy 부하 분산 장치 뒤 hello 구성:</span><span class="sxs-lookup"><span data-stu-id="22cd0-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="22cd0-114">프런트 엔드 IP 구성: 들어오는 네트워크 트래픽에 대한 공용 IP(PIP) 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="22cd0-115">백 엔드 주소 풀: hello hello 부하 분산 장치에서 tooreceive 네트워크 트래픽을 가상 컴퓨터에 대 한 Nic (네트워크 인터페이스)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-115">Back-end address pool: contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="22cd0-116">부하 분산 규칙: hello 백 엔드 주소 풀의 hello 부하 분산 장치 tooa 포트에 공용 포트를 매핑하는 규칙을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-116">Load-balancing rules: contains rules that map a public port on hello load balancer tooa port in hello back-end address pool.</span></span>
* <span data-ttu-id="22cd0-117">인바운드 NAT 규칙: hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트를 매핑하는 규칙을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-117">Inbound NAT rules: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="22cd0-118">프로브: hello 백 엔드 주소 풀의 가상 컴퓨터 인스턴스 중 사용 된 검색 toocheck 가용성 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-118">Probes: contains health probes used toocheck availability of virtual machine instances in hello back-end address pool.</span></span>

<span data-ttu-id="22cd0-119">자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22cd0-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="22cd0-120">PowerShell toouse 리소스 관리자 설정</span><span class="sxs-lookup"><span data-stu-id="22cd0-120">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="22cd0-121">PowerShell에 대 한 hello Azure 리소스 관리자 모듈의 최신 프로덕션 버전 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-121">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="22cd0-122">TooAzure에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-122">Sign in tooAzure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="22cd0-123">메시지가 표시되면 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="22cd0-124">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-124">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="22cd0-125">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-125">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="22cd0-126">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-126">Create a resource group.</span></span> <span data-ttu-id="22cd0-127">(기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뜁니다.)</span><span class="sxs-lookup"><span data-stu-id="22cd0-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="22cd0-128">가상 네트워크 및 hello 프런트 엔드 IP 풀에 대 한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="22cd0-128">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="22cd0-129">서브넷 및 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="22cd0-130">Azure 공용 IP 주소 리소스, 명명 된 만들기 **PublicIP**, hello DNS 이름 사용 하 여 프런트 엔드 IP 풀에서 사용 하는 toobe **loadbalancernrp.westus.cloudapp.azure.com**. 다음 명령을 hello hello를 사용 하 여 정적 할당 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-130">Create an Azure public IP address resource, named **PublicIP**, toobe used by a front-end IP pool with hello DNS name **loadbalancernrp.westus.cloudapp.azure.com**. hello following command uses hello static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="22cd0-131">hello 부하 분산 장치는 해당 FQDN에 대 한 접두사로 hello 공용 IP의 도메인 레이블을 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-131">hello load balancer uses hello domain label of hello public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="22cd0-132">이 hello 부하 분산 장치 FQDN으로 hello 클라우드 서비스를 사용 하 여 hello 클래식 배포 모델에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-132">This is different from hello classic deployment model, which uses hello cloud service as hello load balancer FQDN.</span></span>
   > <span data-ttu-id="22cd0-133">이 예제에서는 hello FQDN은 **loadbalancernrp.westus.cloudapp.azure.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-133">In this example, hello FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="22cd0-134">프런트 엔드 IP 풀 및 백 엔드 주소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="22cd0-134">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="22cd0-135">명명 된 프런트 엔드 IP 풀 만들기 **LB 프런트 엔드** hello를 사용 하 여 **PublicIp** 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-135">Create a front-end IP pool named **LB-Frontend** that uses hello **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="22cd0-136">**LB-backend**라는 백 엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-136">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="22cd0-137">NAT 규칙, 부하 분산 장치 규칙, 프로브 및 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="22cd0-137">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="22cd0-138">이 예에서는 hello 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-138">This example creates hello following items:</span></span>

* <span data-ttu-id="22cd0-139">3389 tooport 3441 포트에서 수신 되는 모든 트래픽을 NAT 규칙 tootranslate</span><span class="sxs-lookup"><span data-stu-id="22cd0-139">A NAT rule tootranslate all incoming traffic on port 3441 tooport 3389</span></span>
* <span data-ttu-id="22cd0-140">3389 tooport 3442 포트에서 수신 되는 모든 트래픽을 NAT 규칙 tootranslate</span><span class="sxs-lookup"><span data-stu-id="22cd0-140">A NAT rule tootranslate all incoming traffic on port 3442 tooport 3389</span></span>
* <span data-ttu-id="22cd0-141">명명 된 페이지에는 프로브 규칙 toocheck hello 상태 상태 **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="22cd0-141">A probe rule toocheck hello health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="22cd0-142">부하 분산 장치 규칙 toobalance hello에 포트 80 tooport 80에 들어오는 모든 트래픽을 hello 백 엔드 풀의 주소</span><span class="sxs-lookup"><span data-stu-id="22cd0-142">A load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool</span></span>
* <span data-ttu-id="22cd0-143">이러한 개체를 모두 사용하는 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="22cd0-143">A load balancer that uses all these objects</span></span>

<span data-ttu-id="22cd0-144">다음 단계를 사용:</span><span class="sxs-lookup"><span data-stu-id="22cd0-144">Use these steps:</span></span>

1. <span data-ttu-id="22cd0-145">Hello NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-145">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="22cd0-146">상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-146">Create a health probe.</span></span> <span data-ttu-id="22cd0-147">두 가지 방법으로 tooconfigure는 프로브</span><span class="sxs-lookup"><span data-stu-id="22cd0-147">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="22cd0-148">HTTP 프로브</span><span class="sxs-lookup"><span data-stu-id="22cd0-148">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="22cd0-149">TCP 프로브</span><span class="sxs-lookup"><span data-stu-id="22cd0-149">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="22cd0-150">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-150">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="22cd0-151">이전에 만든 hello 개체를 사용 하 여 hello 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-151">Create hello load balancer by using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="22cd0-152">NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="22cd0-152">Create NICs</span></span>

<span data-ttu-id="22cd0-153">네트워크 인터페이스 만들기 (또는 기존 템플릿을 수정할) 다음 tooNAT 규칙, 부하 분산 장치 규칙 및 프로브 연결:</span><span class="sxs-lookup"><span data-stu-id="22cd0-153">Create network interfaces (or modify existing ones) and then associate them tooNAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="22cd0-154">Hello Nic 만든 toobe 이곳 hello 가상 네트워크 및 가상 네트워크 서브넷 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-154">Get hello virtual network and a virtual network subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="22cd0-155">명명 된 NIC를 만들고 **lb nic1 수**, 첫 번째 NAT 규칙 hello 및 hello 첫 번째 (및만) 백 엔드 주소 풀과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-155">Create a NIC named **lb-nic1-be**, and associate it with hello first NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="22cd0-156">명명 된 NIC를 만들고 **lb nic2 수**, 두 번째 NAT 규칙의 hello 및 hello 첫 번째 (및만) 백 엔드 주소 풀과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-156">Create a NIC named **lb-nic2-be**, and associate it with hello second NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="22cd0-157">Hello Nic를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-157">Check hello NICs.</span></span>

        $backendnic1

    <span data-ttu-id="22cd0-158">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="22cd0-158">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="22cd0-159">사용 하 여 hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello Nic toodifferent Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-159">Use hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NICs toodifferent VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="22cd0-160">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="22cd0-160">Create a virtual machine</span></span>

<span data-ttu-id="22cd0-161">가상 컴퓨터 만들기 및 NIC 할당에 대한 지침은 [PowerShell을 사용하여Azure VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22cd0-161">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface-toohello-load-balancer"></a><span data-ttu-id="22cd0-162">Hello 네트워크 인터페이스 toohello 부하 분산 장치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-162">Add hello network interface toohello load balancer</span></span>

1. <span data-ttu-id="22cd0-163">Azure에서 hello 부하 분산 장치를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-163">Retrieve hello load balancer from Azure.</span></span>

    <span data-ttu-id="22cd0-164">(아직 수행 하지 않은) 하는 경우 변수를 hello 부하 분산 장치 리소스를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-164">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="22cd0-165">hello 변수 라고 **$lb**합니다. Hello 앞에서 만든 hello 부하 분산 장치 리소스에서 동일한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-165">hello variable is called **$lb**. Use hello same names from hello load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="22cd0-166">Hello 백 엔드로 구성 tooa 변수를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-166">Load hello back-end configuration tooa variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="22cd0-167">변수를 이미 만든 hello 네트워크 인터페이스를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-167">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="22cd0-168">변수 이름이 hello **$nic**합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-168">hello variable name is **$nic**.</span></span> <span data-ttu-id="22cd0-169">hello 네트워크 인터페이스 이름을 hello 동일한 hello에서 앞의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-169">hello network interface name is hello same one from hello earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="22cd0-170">Hello 네트워크 인터페이스에서 hello 백 엔드 구성을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-170">Change hello back-end configuration on hello network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="22cd0-171">Hello 네트워크 인터페이스 개체를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-171">Save hello network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="22cd0-172">네트워크 인터페이스 toohello 부하 분산 장치 백 엔드 풀을 추가한 다음 해당 부하 분산 장치 리소스에 대 한 hello 부하 분산 규칙에 따라 네트워크 트래픽을 받기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-172">After a network interface is added toohello load balancer back-end pool, it starts receiving network traffic based on hello load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="22cd0-173">기존 부하 분산 장치 업데이트</span><span class="sxs-lookup"><span data-stu-id="22cd0-173">Update an existing load balancer</span></span>

1. <span data-ttu-id="22cd0-174">Hello를 사용 하 여 부하를 분산 장치를 부하 분산 장치 개체 toohello 변수를 지정 하는 앞의 예제 hello **$slb** 를 사용 하 여 `Get-AzureLoadBalancer`합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-174">By using hello load balancer from hello earlier example, assign a load balancer object toohello variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="22cd0-175">다음 예제는 hello, hello 백 엔드 풀-tooan 기존 부하 분산 장치에 대 한 포트 81 hello 프런트 엔드 풀에서 및 8181 포트를 사용 하 여 인바운드 NAT 규칙-를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-175">In hello following example, you add an inbound NAT rule--by using port 81 in hello front-end pool and port 8181 for hello back-end pool--tooan existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="22cd0-176">사용 하 여 hello 새 구성을 저장 `Set-AzureLoadBalancer`합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-176">Save hello new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="22cd0-177">부하 분산 장치 제거하기</span><span class="sxs-lookup"><span data-stu-id="22cd0-177">Remove a load balancer</span></span>

<span data-ttu-id="22cd0-178">Hello 명령을 사용 하 여 `Remove-AzureLoadBalancer` toodelete 명명 된 이전에 만든된 부하 분산 장치 **NRP LB** 리소스 그룹에 호출 **NRP RG**합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-178">Use hello command `Remove-AzureLoadBalancer` toodelete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="22cd0-179">Hello 선택적 스위치를 사용 하면 **-Force** tooavoid hello 메시지 삭제를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="22cd0-179">You can use hello optional switch **-Force** tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22cd0-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22cd0-180">Next steps</span></span>

[<span data-ttu-id="22cd0-181">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="22cd0-181">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="22cd0-182">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="22cd0-182">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="22cd0-183">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="22cd0-183">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
