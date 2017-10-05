---
title: "웹 응용 프로그램 방화벽 구성 - Azure Application Gateway | Microsoft Docs"
description: "이 문서에서는 기존 또는 새 Application Gateway에 웹 응용 프로그램 방화벽을 사용하는 방법을 안내합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="97c5e-103">새 또는 기존 Application Gateway에 웹 응용 프로그램 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="97c5e-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="97c5e-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="97c5e-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="97c5e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97c5e-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="97c5e-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="97c5e-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="97c5e-107">웹 응용 프로그램 방화벽을 사용하도록 설정된 Application Gateway를 만들거나 기존 Application Gateway에 웹 응용 프로그램 방화벽을 추가하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="97c5e-108">Azure Application Gateway의 웹 응용 프로그램 방화벽(WAF)은 SQL 삽입 공격, 사이트 간 스크립팅 공격, 세션 하이재킹 등의 일반적인 웹 기반 공격으로부터 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="97c5e-109">Azure Application Gateway는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="97c5e-110">클라우드 또는 온-프레미스이든 상관없이 서로 다른 서버 간에 장애 조치(Failover), 성능 라우팅 HTTP 요청을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="97c5e-111">Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="97c5e-112">지원되는 기능의 전체 목록을 찾으려면 [Application Gateway에 대한 개요](application-gateway-introduction.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="97c5e-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="97c5e-113">다음 문서에서는 [기존 Application Gateway에 웹 응용 프로그램 방화벽 추가](#add-web-application-firewall-to-an-existing-application-gateway) 및 [웹 응용 프로그램 방화벽을 사용하는 Application Gateway 만들기](#create-an-application-gateway-with-web-application-firewall)에 대해 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![시나리오 이미지][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="97c5e-115">WAF 구성 차이</span><span class="sxs-lookup"><span data-stu-id="97c5e-115">WAF configuration differences</span></span>

<span data-ttu-id="97c5e-116">[PowerShell을 사용하여 Application Gateway 만들기](application-gateway-create-gateway-arm.md)를 읽어 보셨다면 Application Gateway를 만들 때 구성하는 SKU 설정에 대해 알고 계실 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="97c5e-117">WAF는 Application Gateway에 SKU를 구성할 때 정의하는 추가 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="97c5e-118">Application Gateway 자체에서 추가로 변경해야 하는 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="97c5e-119">**설정**</span><span class="sxs-lookup"><span data-stu-id="97c5e-119">**Setting**</span></span> | <span data-ttu-id="97c5e-120">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="97c5e-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="97c5e-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="97c5e-121">**SKU**</span></span> |<span data-ttu-id="97c5e-122">WAF가 없는 일반 Application Gateway는 **Standard\_Small**, **Standard\_Medium** 및 **Standard\_Large** 크기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="97c5e-123">WAF의 도입으로 두 개의 SKU, 즉 **WAF\_Medium** 및 **WAF\_Large** SKU가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="97c5e-124">소형 Application Gateway에는 WAF가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="97c5e-125">**계층**</span><span class="sxs-lookup"><span data-stu-id="97c5e-125">**Tier**</span></span> | <span data-ttu-id="97c5e-126">사용 가능한 값은 **표준** 또는 **WAF**입니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="97c5e-127">웹 응용 프로그램 방화벽을 사용하는 경우 **WAF**를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="97c5e-128">**모드**</span><span class="sxs-lookup"><span data-stu-id="97c5e-128">**Mode**</span></span> | <span data-ttu-id="97c5e-129">이 설정은 WAF 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="97c5e-130">허용되는 값은 **검색** 및 **방지**입니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="97c5e-131">WAF를 검색 모드로 설정하면 모든 위협이 로그 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="97c5e-132">방지 모드에서는 이벤트를 여전히 기록하지만 공격자가 Application Gateway로부터 403 권한 없음 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="97c5e-133">기존 Application Gateway에 웹 응용 프로그램 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="97c5e-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="97c5e-134">Azure PowerShell의 최신 버전을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="97c5e-135">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97c5e-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="97c5e-136">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="97c5e-137">이 시나리오에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="97c5e-138">웹 응용 프로그램 방화벽을 추가하려는 게이트웨이를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="97c5e-139">웹 응용 프로그램 방화벽 sku를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="97c5e-140">사용 가능한 크기는 **WAF\_Large** 및 **WAF\_Medium**입니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="97c5e-141">웹 응용 프로그램 방화벽을 사용하는 경우 계층은 **WAF**여야 하며, sku를 설정하는 경우 용량을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="97c5e-142">다음 예제에 정의된 대로 WAF 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="97c5e-143">**FirewallMode**의 경우 사용 가능한 값은 방지 및 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="97c5e-144">이전 단계에서 정의한 설정을 사용하여 Application Gateway를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="97c5e-145">이 명령은 웹 응용 프로그램 방화벽이 있는 Application Gateway를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="97c5e-146">[Application Gateway 진단](application-gateway-diagnostics.md)을 방문하여 응용 프로그램 게이트웨이에 대한 로그를 보는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="97c5e-147">WAF의 보안 특성상, 주기적으로 로그를 검토하여 웹 응용 프로그램의 보안 상태를 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="97c5e-148">웹 응용 프로그램 방화벽이 있는 Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="97c5e-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="97c5e-149">다음 단계에서는 웹 응용 프로그램 방화벽이 있는 Application Gateway를 만드는 전체 과정을 처음부터 끝까지 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="97c5e-150">Azure PowerShell의 최신 버전을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="97c5e-151">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97c5e-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="97c5e-152">`Login-AzureRmAccount`를 실행하여 Azure에 로그인하면 자격 증명을 사용하여 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="97c5e-153">`Get-AzureRmSubscription`을 실행하여 계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="97c5e-154">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="97c5e-155">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="97c5e-155">Create a resource group</span></span>

<span data-ttu-id="97c5e-156">Application Gateway에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="97c5e-157">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="97c5e-158">이 위치는 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="97c5e-159">Application Gateway를 만드는 모든 명령이 동일한 리소스 그룹을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="97c5e-160">이전 예제에서는 "appgw-RG"라는 리소스 그룹과 "미국 서부"라는 위치를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="97c5e-161">Application Gateway에 사용자 지정 프로브를 구성해야 하는 경우 [PowerShell을 사용하여 사용자 지정 프로브로 Application Gateway 만들기](application-gateway-create-probe-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97c5e-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="97c5e-162">자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md) 을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="97c5e-163">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="97c5e-163">Configure virtual network</span></span>

<span data-ttu-id="97c5e-164">Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="97c5e-165">이 단계에서는 10.0.0.0/16 주소 공간과 두 서브넷(Application Gateway에 하나 및 백 엔드 풀 멤버에 하나)을 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="97c5e-166">공용 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="97c5e-166">Configure public IP address</span></span>

<span data-ttu-id="97c5e-167">외부 요청을 처리하기 위해 Application Gateway에는 공용 IP 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="97c5e-168">이 공용 IP 주소에는 Application Gateway에서 사용되도록 정의된 `DomainNameLabel`이 있어서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="97c5e-169">Application Gateway 구성</span><span class="sxs-lookup"><span data-stu-id="97c5e-169">Configure the Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="97c5e-170">기본 웹 응용 프로그램 방화벽 구성을 사용하여 만든 Application Gateway는 보호를 위해 CRS 3.0으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="97c5e-171">Application Gateway DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="97c5e-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="97c5e-172">게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="97c5e-173">공용 IP를 사용할 때 Application Gateway는 친근한 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="97c5e-174">최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="97c5e-175">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="97c5e-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="97c5e-176">별칭을 구성하려면 Application Gateway에 연결된 PublicIPAddress 요소를 사용하여 Application Gateway 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="97c5e-177">Application Gateway의 DNS 이름은 두 개의 웹 응용 프로그램을 이 DNS 이름으로 가리키는 CNAME 레코드를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="97c5e-178">A 레코드를 사용할 경우 Application Gateway 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97c5e-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="97c5e-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97c5e-179">Next steps</span></span>

<span data-ttu-id="97c5e-180">[Application Gateway 진단](application-gateway-diagnostics.md)을 방문하여 진단 로깅을 구성하는 방법 및 웹 응용 프로그램 방화벽을 통해 검색 또는 방지되는 이벤트를 기록하는 방법에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="97c5e-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
