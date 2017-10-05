---
title: "사용자 지정 프로브 만들기 - Azure Application Gateway - PowerShell | Microsoft Docs"
description: "리소스 관리자에서 PowerShell을 사용하여 응용 프로그램 게이트웨이에 대한 사용자 지정 프로브를 만드는 방법에 대해 알아봅니다."
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: b54fe5267d87a41eb9e81d5d1dc9b1b16c5c5e88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="b53fe-103">Azure 리소스 관리자에 대해 PowerShell을 사용하여 Azure 응용 프로그램 게이트웨이에 대한 사용자 지정 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="b53fe-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b53fe-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="b53fe-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="b53fe-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="b53fe-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="b53fe-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="b53fe-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="b53fe-107">이 문서에서는 PowerShell을 사용하여 기존 응용 프로그램 게이트웨이에 사용자 지정 프로브를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="b53fe-108">사용자 지정 프로브는 특정 상태 확인 페이지를 사용하는 응용 프로그램이나 기본 웹 응용 프로그램에서 성공적으로 응답을 제공하지 않는 응용 프로그램에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="b53fe-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b53fe-110">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 [클래식 배포 모델](application-gateway-create-probe-classic-ps.md) 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="b53fe-111">사용자 지정 프로브를 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="b53fe-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="b53fe-112">로그인하여 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b53fe-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="b53fe-113">`Login-AzureRmAccount`을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-113">Use `Login-AzureRmAccount` to authenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="b53fe-114">계정에 대한 구독을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-114">Get the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="b53fe-115">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-115">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="b53fe-116">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-116">Create a resource group.</span></span> <span data-ttu-id="b53fe-117">기존 리소스 그룹을 사용하는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="b53fe-118">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="b53fe-119">이 위치는 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-119">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="b53fe-120">응용 프로그램 게이트웨이를 만들기 위한 모든 명령이 동일한 리소스 그룹을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-120">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="b53fe-121">이전 예제에서는 **West US** 위치에 **appgw-RG**라는 리소스 그룹을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-121">In the preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="b53fe-122">가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="b53fe-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="b53fe-123">다음 예제에서는 응용 프로그램 게이트웨이에 대한 가상 네트워크와 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-123">The following example creates a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="b53fe-124">응용 프로그램 게이트웨이에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="b53fe-125">이러한 이유로 응용 프로그램 게이트웨이를 위해 만드는 서브넷은 VNET의 주소 공간보다 작아야 다른 서브넷을 만들고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-125">For this reason, the subnet created for the application gateway should be smaller than the address space of the VNET to allow for other subnets to be created and used.</span></span>

```powershell
# Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for the next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="b53fe-126">프런트 엔드 구성에 대한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="b53fe-126">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="b53fe-127">미국 서부 지역에 리소스 그룹 **appgw-rg**에서 공용 IP 리소스 **publicIP01**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="b53fe-128">이 예제에서는 응용 프로그램 게이트웨이의 프런트 엔드 IP 주소에 공용 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-128">This example uses a public IP address for the front-end IP address of the application gateway.</span></span>  <span data-ttu-id="b53fe-129">응용 프로그램 게이트웨이를 사용하려면 공용 IP 주소에 동적으로 만들어진 DNS 이름이 있어야 하므로 공용 IP 주소를 만드는 동안에는 `-DomainNameLabel`을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-129">Application gateway requires the public IP address to have a dynamically created DNS name therefore the `-DomainNameLabel` cannot be specified during the creation of the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="b53fe-130">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="b53fe-130">Create an application gateway</span></span>

<span data-ttu-id="b53fe-131">Application Gateway를 만들기 전에 모든 구성 항목을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-131">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="b53fe-132">다음 예제에서는 응용 프로그램 게이트웨이 리소스에 필요한 구성 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-132">The following example creates the configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="b53fe-133">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="b53fe-133">**Component**</span></span> | <span data-ttu-id="b53fe-134">**설명**</span><span class="sxs-lookup"><span data-stu-id="b53fe-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="b53fe-135">**게이트웨이 IP 구성**</span><span class="sxs-lookup"><span data-stu-id="b53fe-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="b53fe-136">응용 프로그램 게이트웨이에 대한 IP 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="b53fe-137">**백 엔드 풀**</span><span class="sxs-lookup"><span data-stu-id="b53fe-137">**Backend pool**</span></span> | <span data-ttu-id="b53fe-138">웹 응용 프로그램을 호스팅하는 응용 프로그램 서버에 대한 IP 주소, FQDN 또는 NIC의 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-138">A pool of IP addresses, FQDN's, or NICs that are to the application servers that host the web application</span></span>|
| <span data-ttu-id="b53fe-139">**상태 프로브**</span><span class="sxs-lookup"><span data-stu-id="b53fe-139">**Health probe**</span></span> | <span data-ttu-id="b53fe-140">백 엔드 풀 멤버의 상태를 모니터링하는 데 사용되는 사용자 지정 프로브입니다</span><span class="sxs-lookup"><span data-stu-id="b53fe-140">A custom probe used to monitor the health of the backend pool members</span></span>|
| <span data-ttu-id="b53fe-141">**HTTP 설정**</span><span class="sxs-lookup"><span data-stu-id="b53fe-141">**HTTP settings**</span></span> | <span data-ttu-id="b53fe-142">포트, 프로토콜, 쿠키 기반 선호도, 프로브 및 시간 제한을 포함한 설정의 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="b53fe-143">이러한 설정은 트래픽이 백 엔드 풀 멤버로 라우팅되는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-143">These settings determine how traffic is routed to the backend pool members</span></span>|
| <span data-ttu-id="b53fe-144">**프런트 엔드 포트**</span><span class="sxs-lookup"><span data-stu-id="b53fe-144">**Frontend port**</span></span> | <span data-ttu-id="b53fe-145">응용 프로그램 게이트웨이에서 트래픽을 수신 대기하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-145">The port that the application gateway listens for traffic on</span></span>|
| <span data-ttu-id="b53fe-146">**수신기**</span><span class="sxs-lookup"><span data-stu-id="b53fe-146">**Listener**</span></span> | <span data-ttu-id="b53fe-147">프로토콜, 프론트 엔드 IP 구성 및 프론트 엔드 포트의 조합이며,</span><span class="sxs-lookup"><span data-stu-id="b53fe-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="b53fe-148">들어오는 요청을 수신 대기하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="b53fe-149">**규칙**</span><span class="sxs-lookup"><span data-stu-id="b53fe-149">**Rule**</span></span>| <span data-ttu-id="b53fe-150">HTTP 설정에 따라 트래픽을 적절한 백 엔드로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-150">Routes the traffic to the appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates the backend http settings to be used. This component references the $probe created in the previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for the application gateway to listen on port 80 that will be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates the $publicip variable defined previously with the front-end IP that will be used by the listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates the listener. The listener is a combination of protocol and the frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates the rule that routes traffic to the backend pools.  In this example we create a basic rule that uses the previous defined http settings and backend address pool.  It also associates the listener to the rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets the SKU of the application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# The final step creates the application gateway with all the previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="b53fe-151">기존 응용 프로그램 게이트웨이에 프로브 추가</span><span class="sxs-lookup"><span data-stu-id="b53fe-151">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="b53fe-152">다음 코드 조각에서는 기존 응용 프로그램 게이트웨이에 프로브를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-152">The following code snippet adds a probe to an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create the probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set the backend HTTP settings to use the new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="b53fe-153">기존 응용 프로그램 게이트웨이에서 프로브 제거</span><span class="sxs-lookup"><span data-stu-id="b53fe-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="b53fe-154">다음 코드 조각에서는 기존 응용 프로그램 게이트웨이에서 프로브를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-154">The following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove the probe from the application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set the backend HTTP settings to remove the reference to the probe. The backend http settings now use the default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="b53fe-155">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="b53fe-155">Get application gateway DNS name</span></span>

<span data-ttu-id="b53fe-156">게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-156">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="b53fe-157">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="b53fe-158">최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-158">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="b53fe-159">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b53fe-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="b53fe-160">이 작업을 수행하려면 Application Gateway에 연결된 PublicIPAddress 요소를 사용하여 Application Gateway 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="b53fe-161">응용 프로그램 게이트웨이의 DNS 이름은 두 개의 웹 응용 프로그램을 이 DNS 이름으로 가리키는 CNAME 레코드를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-161">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="b53fe-162">A 레코드를 사용할 경우 응용 프로그램 게이트웨이 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="b53fe-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b53fe-163">Next steps</span></span>

<span data-ttu-id="b53fe-164">[SSL 오프로드 구성](application-gateway-ssl-arm.md)을 방문하여 SSL 오프로드를 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b53fe-164">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

