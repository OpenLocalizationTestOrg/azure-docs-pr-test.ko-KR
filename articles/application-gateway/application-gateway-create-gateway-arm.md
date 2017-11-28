---
title: "aaaCreate 및 Azure 응용 프로그램 게이트웨이-PowerShell 관리 | Microsoft Docs"
description: "이 페이지에서는 toocreate, 구성, 시작 및 Azure 리소스 관리자를 사용 하 여 Azure 응용 프로그램 게이트웨이 삭제 하는 지침을 제공 합니다."
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
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="652f6-103">Azure 리소스 관리자를 사용하여 응용 프로그램 게이트웨이 만들기, 시작 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="652f6-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="652f6-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="652f6-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="652f6-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="652f6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="652f6-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="652f6-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="652f6-107">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="652f6-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="652f6-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="652f6-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="652f6-109">Azure Application Gateway는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="652f6-110">Hello 클라우드 또는 온-프레미스에 있는지 여부를 장애 조치 및 다른 서버 간에 HTTP 요청 성능 라우팅을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="652f6-111">Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="652f6-112">지원 되는 기능의 전체 목록은 toofind 방문 [응용 프로그램 게이트웨이 개요](application-gateway-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="652f6-113">이 문서 단계별로 hello 단계 toocreate, 구성, 시작 및 응용 프로그램 게이트웨이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="652f6-114">Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: 리소스 관리자 및 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-114">Before you work with Azure resources, it is important toounderstand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="652f6-115">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md)를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="652f6-116">이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-116">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="652f6-117">이 문서에서는 Azure Resource Manager를 사용하여 응용 프로그램 게이트웨이 만들기를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="652f6-118">toouse hello 클래식 버전 너무 이동[PowerShell을 사용 하 여 응용 프로그램 게이트웨이 클래식 배포를 만들](application-gateway-create-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-118">toouse hello classic version, go too[Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="652f6-119">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="652f6-119">Before you begin</span></span>

1. <span data-ttu-id="652f6-120">Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="652f6-121">다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="652f6-122">기존 가상 네트워크를 사용 하도록 설정한 경우 기존 빈 서브넷을 선택 하거나 hello 응용 프로그램 게이트웨이에서 사용 하기 위해서만 기존 가상 네트워크의 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="652f6-123">Hello 응용 프로그램 게이트웨이 tooa 다른 가상 네트워크를 배포할 수 없습니다 하려는 hello 응용 프로그램 게이트웨이 뒤 toodeploy hello 리소스 보다 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-123">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway.</span></span>
1. <span data-ttu-id="652f6-124">toouse hello 응용 프로그램 게이트웨이 구성 하는 hello 서버에 존재 해야 하거나 또는 hello 가상 네트워크에서 공용 IP/VIP와 만든 끝점을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-124">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="652f6-125">필요한 toocreate 응용 프로그램 게이트웨이 란?</span><span class="sxs-lookup"><span data-stu-id="652f6-125">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="652f6-126">**백 엔드 서버 풀:** IP 주소, Fqdn 또는 hello 백 엔드 서버의 Nic의 hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-126">**Backend server pool:** hello list of IP addresses, FQDNs, or NICs of hello backend servers.</span></span> <span data-ttu-id="652f6-127">IP 주소를 사용 하면은 해야 하거나 toohello 가상 네트워크 서브넷 속하거나, 공용 IP/VIP가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-127">If IP addresses are used, they should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="652f6-128">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="652f6-129">이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="652f6-130">**프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-130">**frontend port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="652f6-131">트래픽이이 포트에 도달 하 고 hello 백 엔드 서버의 리디렉션된 tooone 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-131">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="652f6-132">**수신기:** hello 수신기에 프런트 엔드 포트, 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="652f6-132">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="652f6-133">**규칙:** hello 규칙 hello 수신기를 hello 백 엔드 서버 풀에 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-133">**Rule:** hello rule binds hello listener, hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="652f6-134">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="652f6-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="652f6-135">Hello 최신 버전의 Azure PowerShell을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-135">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="652f6-136">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="652f6-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="652f6-137">TooAzure를 로그인 하 고 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-137">Log in tooAzure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="652f6-138">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-138">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="652f6-139">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-139">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="652f6-140">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="652f6-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="652f6-141">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="652f6-142">이 위치는 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-142">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="652f6-143">응용 프로그램 게이트웨이 사용 하 여 모든 명령을 toocreate hello 동일 하 고 있는지 확인 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-143">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="652f6-144">리소스 그룹이 위의 hello 예제에서 만든 **ContosoRG** 및 위치 **미국 동부**합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-144">In hello example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="652f6-145">응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브 tooconfigure 필요 하면 방문: [PowerShell을 사용 하 여 사용자 지정 프로브 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-probe-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-145">If you need tooconfigure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="652f6-146">자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md) 을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-hello-application-gateway-configuration-objects"></a><span data-ttu-id="652f6-147">구성 개체 hello 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="652f6-147">Create hello application gateway configuration objects</span></span>

<span data-ttu-id="652f6-148">Hello 응용 프로그램 게이트웨이 만들기 전에 모든 구성 항목 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-148">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="652f6-149">hello 다음 단계 hello 구성 항목을 만드는 응용 프로그램 게이트웨이 리소스에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-149">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="652f6-150">완료 되 면 hello 공용 IP 리소스 toohello 연결 된 응용 프로그램 게이트웨이에서 DNS 및 VIP hello 응용 프로그램 게이트웨이 세부 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-150">When complete, retrieve DNS and VIP details of hello application gateway from hello public IP resource attached toohello application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="652f6-151">Hello 응용 프로그램 게이트웨이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-151">Delete hello application gateway</span></span>

<span data-ttu-id="652f6-152">hello 다음 삭제 하는 예제 응용 프로그램 게이트웨이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-152">hello following example deletes hello application gateway.</span></span>

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="652f6-153">hello **-강제로** 스위치 사용된 toosuppress hello 제거 확인 메시지를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-153">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="652f6-154">서비스 hello tooverify 제거 된 hello를 사용할 수 있습니다, `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="652f6-154">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="652f6-155">이 단계는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="652f6-156">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="652f6-156">Get application gateway DNS name</span></span>

<span data-ttu-id="652f6-157">Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-157">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="652f6-158">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="652f6-159">tooensure 최종 사용자가 hello 응용 프로그램 게이트웨이 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello hello 응용 프로그램 게이트웨이의 공용 끝점 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-159">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="652f6-160">toodo hello 응용 프로그램 게이트웨이 및 연결 된 해당 IP/DNS 이름 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여이 검색 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="652f6-161">이렇게 Azure DNS 또는 기타 DNS 공급자에서 toohello 가리키는 CNAME 레코드를 만들어 [공용 IP 주소](../dns/dns-custom-domain.md#public-ip-address)합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="652f6-162">A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="652f6-163">IP 주소는 hello 서비스가 시작 될 때 toohello 응용 프로그램 게이트웨이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-163">An IP address is assigned toohello application gateway when hello service starts.</span></span>

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

## <a name="delete-all-resources"></a><span data-ttu-id="652f6-164">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="652f6-164">Delete all resources</span></span>

<span data-ttu-id="652f6-165">이 문서의 단계 다음에 나오는 전체 hello 만든 모든 리소스를 toodelete:</span><span class="sxs-lookup"><span data-stu-id="652f6-165">toodelete all resources created in this article, complete hello following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="652f6-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="652f6-166">Next steps</span></span>

<span data-ttu-id="652f6-167">SSL 오프 로드 tooconfigure 방문: [SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-167">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="652f6-168">내부 부하 분산 장치는 응용 프로그램 게이트웨이 toouse tooconfigure 방문: [내부 부하 분산 장치 (ILB) 응용 프로그램 게이트웨이 만들](application-gateway-ilb.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="652f6-168">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="652f6-169">부하 분산 옵션에 대한 자세한 정보는 다음을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="652f6-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="652f6-170">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="652f6-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="652f6-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="652f6-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
