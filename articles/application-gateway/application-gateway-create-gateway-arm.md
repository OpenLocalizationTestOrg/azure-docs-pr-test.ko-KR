---
title: "Azure Application Gateway 만들기 및 관리 - PowerShell | Microsoft Docs"
description: "이 페이지에서는 Azure Resource Manager를 사용하여 Azure 응용 프로그램 게이트웨이를 만들고, 구성하고, 시작하고, 삭제하기 위한 지침을 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 5f1713365406764998de505ff62309bab9fa2567
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="bca53-103">Azure 리소스 관리자를 사용하여 응용 프로그램 게이트웨이 만들기, 시작 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="bca53-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bca53-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bca53-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="bca53-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="bca53-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="bca53-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="bca53-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="bca53-107">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="bca53-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="bca53-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bca53-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="bca53-109">Azure 응용 프로그램 게이트웨이는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="bca53-110">클라우드 또는 온-프레미스에 상관없이 서로 다른 서버 간에 장애 조치(failover) 및 성능 라우팅 HTTP 요청을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="bca53-111">Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="bca53-112">지원되는 기능의 전체 목록을 보려면 [Application Gateway 개요](application-gateway-introduction.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="bca53-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="bca53-113">이 문서는 응용 프로그램 게이트웨이를 생성, 구성, 시작 및 삭제하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bca53-114">Azure 리소스로 작업하기 전에 Azure에는 현재 Resource Manager와 클래식 모드의 두 가지 배포 모델이 있다는 것을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-114">Before you work with Azure resources, it is important to understand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="bca53-115">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md)를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="bca53-116">이 문서의 윗부분에 있는 탭을 클릭하여 다양한 도구에 대한 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-116">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="bca53-117">이 문서에서는 Azure Resource Manager를 사용하여 응용 프로그램 게이트웨이 만들기를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="bca53-118">클래식 버전을 사용하려면 [PowerShell을 사용하여 응용 프로그램 게이트웨이 클래식 배포 만들기](application-gateway-create-gateway.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-118">To use the classic version, go to [Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bca53-119">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="bca53-119">Before you begin</span></span>

1. <span data-ttu-id="bca53-120">웹 플랫폼 설치 관리자를 사용하는 Azure PowerShell cmdlet의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="bca53-121">**다운로드 페이지** 의 [Windows PowerShell](https://azure.microsoft.com/downloads/)섹션에서 최신 버전을 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="bca53-122">기존 가상 네트워크가 있는 경우 기존의 빈 서브넷을 선택하거나 응용 프로그램 게이트웨이에서 사용할 기존 가상 네트워크에만 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="bca53-123">응용 프로그램 게이트웨이 뒤에 배포하려는 리소스가 아닌 다른 가상 네트워크에 응용 프로그램 게이트웨이를 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-123">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway.</span></span>
1. <span data-ttu-id="bca53-124">응용 프로그램 게이트웨이를 사용하도록 구성된 서버가 존재하거나 가상 네트워크나 공용 IP/VIP가 할당된 해당 끝점이 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-124">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="bca53-125">응용 프로그램 게이트웨이를 만드는 데 필요한 것은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bca53-125">What is required to create an application gateway?</span></span>

* <span data-ttu-id="bca53-126">**백 엔드 서버 풀:** 백 엔드 서버의 IP 주소, FQDN 또는 NIC 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-126">**Backend server pool:** The list of IP addresses, FQDNs, or NICs of the backend servers.</span></span> <span data-ttu-id="bca53-127">사용되는 IP 주소는 가상 네트워크 서브넷에 속하거나 공용 IP/VIP여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-127">If IP addresses are used, they should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="bca53-128">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="bca53-129">이러한 설정은 풀에 연결 및 풀 내의 모든 서버에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="bca53-130">**프런트 엔드 포트:** 이 포트는 응용 프로그램 게이트웨이에서 열려 있는 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-130">**frontend port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="bca53-131">트래픽이 이 포트에 도달하면, 백엔드 서버 중의 하나가 리디렉트됩니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-131">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="bca53-132">**수신기:** 수신기에는 프런트 엔드 포트, 프로토콜(Http 또는 Https, 이 값은 대/소문자 구분) 및 SSL 인증서 이름(SSL 오프로드를 구성하는 경우)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-132">**Listener:** The listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="bca53-133">**규칙:** 규칙은 수신기와 백 엔드 서버 풀을 바인딩하고 특정 수신기에 도달했을 때 트래픽이 이동되는 백 엔드 서버 풀을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-133">**Rule:** The rule binds the listener, the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="bca53-134">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="bca53-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="bca53-135">Azure PowerShell의 최신 버전을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-135">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="bca53-136">자세한 내용은 [Resource Manager에서 Windows PowerShell](../powershell-azure-resource-manager.md)사용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bca53-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="bca53-137">Azure에 로그인하여 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-137">Log in to Azure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="bca53-138">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-138">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="bca53-139">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-139">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="bca53-140">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="bca53-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="bca53-141">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="bca53-142">이 위치는 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-142">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="bca53-143">응용 프로그램 게이트웨이를 만들기 위한 모든 명령이 동일한 리소스 그룹을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-143">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="bca53-144">위의 예제에서는 **ContosoRG**라는 리소스 그룹과 **미국 동부**라는 위치를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-144">In the example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="bca53-145">응용 프로그램 게이트웨이에 대한 사용자 지정 프로브를 구성해야 하는 경우 [PowerShell을 사용하여 사용자 지정 프로브로 응용 프로그램 게이트웨이 만들기](application-gateway-create-probe-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bca53-145">If you need to configure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="bca53-146">자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-the-application-gateway-configuration-objects"></a><span data-ttu-id="bca53-147">응용 프로그램 게이트웨이 구성 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="bca53-147">Create the application gateway configuration objects</span></span>

<span data-ttu-id="bca53-148">응용 프로그램 게이트웨이를 만들기 전에 모든 구성 항목을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-148">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="bca53-149">다음 단계 응용 프로그램 게이트웨이 리소스에 필요한 구성 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-149">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign the address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with the address space of 10.0.0.0/16 and add the subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve the newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used to connect to the application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. The gateway picks up an IP addressfrom the configured subnet and routes network traffic to the IP addresses in the backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with the addresses of your web servers. These backend pool members are all validated to be healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed to them when requests come into the application gateway. Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings to determine the protocol and port that is used when sending traffic to the backend servers. Cookie-based sessions are also determined by the backend HTTP settings.  If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used to connect to the application gateway through the public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure the frontend IP configuration with the public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure the listener.  The listener is a combination of the front end IP configuration, protocol, and port and is used to receive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used to route traffic to the backend servers. The backend pool settings, listener, and backend pool created in the previous steps make up the rule. Based on the criteria defined traffic is routed to the appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU for the application gateway, this determines the size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create the application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="bca53-150">완료되면 응용 프로그램 게이트웨이에 연결된 공용 IP 리소스에서 응용 프로그램 게이트웨이의 DNS 및 VIP 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-150">When complete, retrieve DNS and VIP details of the application gateway from the public IP resource attached to the application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="bca53-151">응용 프로그램 게이트웨이 삭제</span><span class="sxs-lookup"><span data-stu-id="bca53-151">Delete the application gateway</span></span>

<span data-ttu-id="bca53-152">다음 예제에서는 응용 프로그램 게이트웨이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-152">The following example deletes the application gateway.</span></span>

```powershell
# Retrieve the application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops the application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="bca53-153">**-force** 스위치를 사용하여 제거 확인 메시지가 표시되지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-153">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="bca53-154">서비스가 제거되었는지 확인하려면 `Get-AzureRmApplicationGateway` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-154">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="bca53-155">이 단계는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="bca53-156">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="bca53-156">Get application gateway DNS name</span></span>

<span data-ttu-id="bca53-157">게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-157">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="bca53-158">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="bca53-159">최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-159">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="bca53-160">이 작업을 수행하려면 Application Gateway에 연결된 PublicIPAddress 요소를 사용하여 Application Gateway 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="bca53-161">이 작업은 [공용 IP 주소](../dns/dns-custom-domain.md#public-ip-address)를 가리키는 CNAME 레코드를 만들어 Azure DNS 또는 다른 DNS 공급자를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points to the [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="bca53-162">A 레코드를 사용할 경우 응용 프로그램 게이트웨이 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="bca53-163">서비스를 시작할 때 응용 프로그램 게이트웨이에 IP 주소가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-163">An IP address is assigned to the application gateway when the service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a><span data-ttu-id="bca53-164">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="bca53-164">Delete all resources</span></span>

<span data-ttu-id="bca53-165">이 문서에서 만든 모든 리소스를 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="bca53-165">To delete all resources created in this article, complete the following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="bca53-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bca53-166">Next steps</span></span>

<span data-ttu-id="bca53-167">SSL 오프로드를 구성하려는 경우 [SSL 오프로드에 대한 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bca53-167">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="bca53-168">내부 부하 분산 장치에서 사용하도록 응용 프로그램 게이트웨이를 구성하려면 [ILB(내부 부하 분산 장치)를 사용하여 응용 프로그램 게이트웨이 만들기](application-gateway-ilb.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bca53-168">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="bca53-169">부하 분산 옵션에 대한 자세한 정보는 다음을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="bca53-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="bca53-170">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="bca53-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="bca53-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="bca53-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
