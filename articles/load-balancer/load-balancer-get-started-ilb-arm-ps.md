---
title: "내부 부하 분산 장치 만들기 - PowerShell | Microsoft Docs"
description: "리소스 관리자에서 PowerShell을 사용하여 내부 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7bd31ab8f52ec5e81f6966000554be46eaa59396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="69c68-103">PowerShell을 사용하여 내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="69c68-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="69c68-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="69c68-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="69c68-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69c68-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="69c68-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="69c68-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="69c68-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="69c68-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="69c68-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="69c68-109">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 [클래식 배포 모델](load-balancer-get-started-ilb-classic-ps.md) 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="69c68-110">다음 단계에서는 PowerShell과 함께 Azure Resource Manager를 사용하여 인터넷 부하 분산 장치를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-110">The following steps explain how to create an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="69c68-111">Azure Resource Manager를 사용하면 내부 부하 분산 장치를 만드는 항목이 개별적으로 구성된 다음 결합되어 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-111">With Azure Resource Manager, the items to create a Internal load balancer are configured individually and then combined to create a load balancer.</span></span>

<span data-ttu-id="69c68-112">부하 분산 장치를 배포하려면 다음 개체를 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-112">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="69c68-113">프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 개인 IP 주소를 구성합니다</span><span class="sxs-lookup"><span data-stu-id="69c68-113">Front end IP configuration - will configure the private IP address for incoming network traffic</span></span>
* <span data-ttu-id="69c68-114">백 엔드 주소 풀 - 프런트 엔드 IP 풀에서 들어오는 부하 분산된 트래픽을 수신하는 네트워크 인터페이스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-114">Backend address pool - will configure the network interfaces which will receive the load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="69c68-115">부하 분산 규칙 - 부하 분산 장치의 원본 및 로컬 포트 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-115">Load balancing rules - source and local port configuration for the load balancer.</span></span>
* <span data-ttu-id="69c68-116">프로브 - 가상 컴퓨터 인스턴스의 상태 프로브를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-116">Probes - configures the health status probe for the Virtual Machine instances.</span></span>
* <span data-ttu-id="69c68-117">인바운드 NAT 규칙 - 가상 컴퓨터 인스턴스 중 하나에 직접 액세스하는 포트 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-117">Inbound NAT rules - configures the port rules to directly access one of the Virtual Machine instances.</span></span>

<span data-ttu-id="69c68-118">Azure 리소스 관리자의 분산 장치 구성 요소에 대한 자세한 내용은 [부하 분산 장치에 대한 Azure 리소스 관리자 지원](load-balancer-arm.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="69c68-119">다음 단계에서는 두 개의 가상 컴퓨터 간에 부하 분산 장치를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-119">The following steps explain how to configure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-to-use-resource-manager"></a><span data-ttu-id="69c68-120">리소스 관리자를 사용하도록 PowerShell 설치</span><span class="sxs-lookup"><span data-stu-id="69c68-120">Setup PowerShell to use Resource Manager</span></span>

<span data-ttu-id="69c68-121">PowerShell용 Azure 모듈이 최신 프로덕션 버전이고 Azure 구독에 액세스하도록 PowerShell이 제대로 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-121">Make sure you have the latest production version of the Azure module for PowerShell, and have PowerShell setup correctly to access your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="69c68-122">1단계</span><span class="sxs-lookup"><span data-stu-id="69c68-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="69c68-123">2단계</span><span class="sxs-lookup"><span data-stu-id="69c68-123">Step 2</span></span>

<span data-ttu-id="69c68-124">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-124">Check the subscriptions for the account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="69c68-125">자격 증명을 사용하여 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-125">You will be prompted to Authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="69c68-126">3단계</span><span class="sxs-lookup"><span data-stu-id="69c68-126">Step 3</span></span>

<span data-ttu-id="69c68-127">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-127">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="69c68-128">부하 분산 장치에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="69c68-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="69c68-129">새 리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="69c68-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="69c68-130">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="69c68-131">이 위치는 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="69c68-132">부하 분산 장치를 만드는 모든 명령에서 동일한 리소스 그룹을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-132">Make sure all commands to create a load balancer will use the same resource group.</span></span>

<span data-ttu-id="69c68-133">위 예제에서는 "NRP-RG"라는 리소스 그룹과 "West US"라는 위치를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-133">In the example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="69c68-134">프런트 엔드 IP 풀에 대한 개인 IP 주소 및 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="69c68-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="69c68-135">가상 네트워크의 서브넷을 만들고 변수 $backendSubnet에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-135">Creates a subnet for the virtual network and assigns to variable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="69c68-136">가상 네트워크 만들기:</span><span class="sxs-lookup"><span data-stu-id="69c68-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="69c68-137">가상 네트워크를 만들고 NRPVNet 가상 네트워크에 lb-subnet-be 서브넷을 추가한 $vnet 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-137">Creates the virtual network and adds the subnet lb-subnet-be to the virtual network NRPVNet and assigns to variable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="69c68-138">프런트 엔드 IP 풀 및 백 엔드 주소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="69c68-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="69c68-139">들어오는 부하 분산 장치 네트워크 트래픽에 대한 프런트 엔드 IP 풀을 설정하고 부하 분산된 트래픽을 수신할 백 엔드 주소 풀을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-139">Setting up a front end IP pool for the incoming load balancer network traffic and backend address pool to receive the load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="69c68-140">1단계</span><span class="sxs-lookup"><span data-stu-id="69c68-140">Step 1</span></span>

<span data-ttu-id="69c68-141">들어오는 네트워크 트래픽 끝점이 될 서브넷 10.0.2.0/24에 대해 개인 IP 주소 10.0.2.5를 사용하여 프런트 엔드 IP 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-141">Create a front end IP pool using the private IP address 10.0.2.5 for the subnet 10.0.2.0/24 which will be the incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="69c68-142">2단계</span><span class="sxs-lookup"><span data-stu-id="69c68-142">Step 2</span></span>

<span data-ttu-id="69c68-143">프런트 엔드 IP 풀에서 들어오는 트래픽을 받는 데 사용되는 백 엔드 주소 풀을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-143">Set up a back end address pool used to receive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="69c68-144">LB 규칙, NAT 규칙, 프로브 및 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="69c68-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="69c68-145">프런트 엔드 IP 풀과 백 엔드 주소 풀을 만든 후에는 부하 분산 장치 리소스에 속하는 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-145">After creating the front end IP pool and the backend address pool, you will need to create the rules which will belong to the load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="69c68-146">1단계</span><span class="sxs-lookup"><span data-stu-id="69c68-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="69c68-147">위 예제에서는 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-147">The example above is creating the following items:</span></span>

* <span data-ttu-id="69c68-148">포트 3441로 들어오는 모든 트래픽을 포트 3389로 이동하는 NAT 규칙</span><span class="sxs-lookup"><span data-stu-id="69c68-148">NAT rule which all incoming traffic to port 3441 will go to port 3389.</span></span>
* <span data-ttu-id="69c68-149">포트 3442로 들어오는 모든 트래픽을 포트 3389로 이동하는 두 번째 NAT 규칙</span><span class="sxs-lookup"><span data-stu-id="69c68-149">a second NAT rule which all incoming traffic to port 3442 will go to port 3389.</span></span>
* <span data-ttu-id="69c68-150">공용 포트 80의 들어오는 모든 트래픽을 백엔드 주소 풀의 로컬 포트 80으로 부하 분산하는 부하 분산 장치 규칙</span><span class="sxs-lookup"><span data-stu-id="69c68-150">a load balancer rule which will load balance all incoming traffic on public port 80 to local port 80 in the back end address pool.</span></span>
* <span data-ttu-id="69c68-151">경로 "HealthProbe.aspx"에 대한 상태를 확인하는 프로브 규칙</span><span class="sxs-lookup"><span data-stu-id="69c68-151">a probe rule which will check the health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="69c68-152">2단계</span><span class="sxs-lookup"><span data-stu-id="69c68-152">Step 2</span></span>

<span data-ttu-id="69c68-153">모든 개체(NAT 규칙, 부하 분산 장치 규칙, 프로브 구성)를 함께 추가하는 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-153">Create the load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="69c68-154">네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="69c68-154">Create network interfaces</span></span>

<span data-ttu-id="69c68-155">내부 부하 분산 장치를 만든 후에는 들어오는 부하 분산된 네트워크 트래픽, NAT 규칙 및 프로브를 수신할 네트워크 인터페이스를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-155">After creating the internal load balancer, you need define which network interfaces will be receiving the incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="69c68-156">이 경우 네트워크 인터페이스는 개별적으로 구성되며 나중에 가상 컴퓨터에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-156">The network interface in this case is configured individually and can be assigned to a virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="69c68-157">1단계</span><span class="sxs-lookup"><span data-stu-id="69c68-157">Step 1</span></span>

<span data-ttu-id="69c68-158">네트워크 인터페이스를 만들 리소스 가상 네트워크 및 서브넷 가져오기:</span><span class="sxs-lookup"><span data-stu-id="69c68-158">Get the resource virtual network and subnet to create network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="69c68-159">이 단계에서는 부하 분산 장치 백 엔드 풀에 속하는 네트워크 인터페이스를 만들고 이 네트워크 인터페이스의 RDP에 대한 첫 번째 NAT 규칙을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-159">This step creates a network interface which will belong to the load balancer back end pool and associate the first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="69c68-160">2단계</span><span class="sxs-lookup"><span data-stu-id="69c68-160">Step 2</span></span>

<span data-ttu-id="69c68-161">LB-Nic2-BE라는 두 번째 네트워크 인터페이스 만들기:</span><span class="sxs-lookup"><span data-stu-id="69c68-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="69c68-162">이 단계에서는 두 번째 네트워크 인터페이스를 만들고 동일한 부하 분산 장치 백 엔드 풀에 할당하고 RDP에 대해 만든 두 번째 NAT 규칙을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-162">This step creates a second network interface, assigning to the same load balancer back end pool and associating the second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="69c68-163">최종 결과는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-163">The end result will show the following:</span></span>

    $backendnic1

<span data-ttu-id="69c68-164">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="69c68-164">Expected output:</span></span>

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a><span data-ttu-id="69c68-165">3단계</span><span class="sxs-lookup"><span data-stu-id="69c68-165">Step 3</span></span>

<span data-ttu-id="69c68-166">Add-AzureRmVMNetworkInterface 명령을 사용하여 가상 컴퓨터에 NIC를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-166">Use the command Add-AzureRmVMNetworkInterface to assign the NIC to a virtual Machine.</span></span>

<span data-ttu-id="69c68-167">가상 컴퓨터를 만드는 단계별 지침을 찾아서 [PowerShell을 사용하여 Azure VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) 문서를 따라 NIC에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-167">You can find the step by step instructions to create a virtual machine and assign to a NIC following the documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface"></a><span data-ttu-id="69c68-168">네트워크 인터페이스 추가</span><span class="sxs-lookup"><span data-stu-id="69c68-168">Add the network interface</span></span>

<span data-ttu-id="69c68-169">이미 가상 컴퓨터를 만든 경우 다음 단계로 네트워크 인터페이스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-169">If you already have a virtual machine created, you can add the network interface with the following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="69c68-170">1단계</span><span class="sxs-lookup"><span data-stu-id="69c68-170">Step 1</span></span>

<span data-ttu-id="69c68-171">(아직 수행하지 않은 경우) 부하 분산 장치 리소스를 변수로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-171">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="69c68-172">사용되는 변수는 $lb라고 하고 위에서 만든 부하 분산 장치 리소스에서 동일한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-172">The variable used is called $lb and use the same names from the load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="69c68-173">2단계</span><span class="sxs-lookup"><span data-stu-id="69c68-173">Step 2</span></span>

<span data-ttu-id="69c68-174">백 엔드 구성을 변수로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-174">Load the backend configuration to a variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="69c68-175">3단계</span><span class="sxs-lookup"><span data-stu-id="69c68-175">Step 3</span></span>

<span data-ttu-id="69c68-176">이미 만든 네트워크 인터페이스를 변수로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-176">Load the already created network interface into a variable.</span></span> <span data-ttu-id="69c68-177">사용되는 변수 이름은 $nic입니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-177">the variable name used is $nic.</span></span> <span data-ttu-id="69c68-178">사용되는 네트워크 인터페이스 이름은 위의 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-178">The network interface name used is the same from the example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="69c68-179">4단계</span><span class="sxs-lookup"><span data-stu-id="69c68-179">Step 4</span></span>

<span data-ttu-id="69c68-180">네트워크 인터페이스에서 백 엔드 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-180">Change the backend configuration on the network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="69c68-181">5단계</span><span class="sxs-lookup"><span data-stu-id="69c68-181">Step 5</span></span>

<span data-ttu-id="69c68-182">네트워크 인터페이스 개체를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-182">Save the network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="69c68-183">네트워크 인터페이스가 부하 분산 장치 백 엔드 풀에 추가된 후 해당 부하 분산 장치 리소스에 대한 부하 분산 규칙에 따라 네트워크 트래픽을 받기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-183">After a network interface is added to the load balancer backend pool, it starts receiving network traffic based on the load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="69c68-184">기존 부하 분산 장치 업데이트</span><span class="sxs-lookup"><span data-stu-id="69c68-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="69c68-185">1단계</span><span class="sxs-lookup"><span data-stu-id="69c68-185">Step 1</span></span>
<span data-ttu-id="69c68-186">위의 예제에서 부하 분산 장치를 사용하여 부하 분산 장치 개체를 Get-AzureRmLoadBalancer를 사용하는 변수 $slb에 할당</span><span class="sxs-lookup"><span data-stu-id="69c68-186">Using the load balancer from the example above, assign load balancer object to variable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="69c68-187">2단계</span><span class="sxs-lookup"><span data-stu-id="69c68-187">Step 2</span></span>

<span data-ttu-id="69c68-188">다음 예제에서는 프런트 엔드에 있는 포트 81과 백 엔드 풀의 포트 8181을 사용하여 새 인바운드 NAT 규칙을 기존 부하 분산 장치에 추가</span><span class="sxs-lookup"><span data-stu-id="69c68-188">In the following example, you will add a new Inbound NAT rule using port 81 in the front end and port 8181 for the back end pool to an existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="69c68-189">3단계</span><span class="sxs-lookup"><span data-stu-id="69c68-189">Step 3</span></span>

<span data-ttu-id="69c68-190">Set-AzureLoadBalancer를 사용하여 새 구성 저장</span><span class="sxs-lookup"><span data-stu-id="69c68-190">Save the new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="69c68-191">부하 분산 장치 제거하기</span><span class="sxs-lookup"><span data-stu-id="69c68-191">Remove a load balancer</span></span>

<span data-ttu-id="69c68-192">Remove-AzureRmLoadBalancer 명령을 사용하여 "NRP-RG"라는 리소스 그룹에서 이전에 생성한 "NRP-LB"라는 부하 분산 장치 삭제</span><span class="sxs-lookup"><span data-stu-id="69c68-192">Use the command Remove-AzureRmLoadBalancer to delete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="69c68-193">선택적 스위치 -Force를 사용하여 삭제에 대한 프롬프트를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c68-193">You can use the optional switch -Force to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69c68-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69c68-194">Next steps</span></span>

[<span data-ttu-id="69c68-195">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="69c68-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="69c68-196">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="69c68-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
