---
title: "aaaCreate 사용자 지정 프로브-Azure 응용 프로그램 게이트웨이-PowerShell | Microsoft Docs"
description: "어떻게 toocreate 사용자 지정 프로브 응용 프로그램 게이트웨이에 대 한 리소스 관리자의 PowerShell을 사용 하 여 알아봅니다"
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
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="908a2-103">Azure 리소스 관리자에 대해 PowerShell을 사용하여 Azure 응용 프로그램 게이트웨이에 대한 사용자 지정 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="908a2-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="908a2-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="908a2-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="908a2-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="908a2-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="908a2-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="908a2-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="908a2-107">이 문서에서는 PowerShell과 함께 사용자 지정 프로브 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="908a2-108">사용자 지정 프로브는 특정 상태 확인 페이지를 사용 하는 응용 프로그램 또는 hello 기본 웹 응용 프로그램에 대 한 성공적인 응답을 제공 하지 않는 응용 프로그램에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="908a2-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="908a2-110">사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](application-gateway-create-probe-classic-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="908a2-111">사용자 지정 프로브를 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="908a2-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="908a2-112">로그인하여 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="908a2-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="908a2-113">사용 하 여 `Login-AzureRmAccount` tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="908a2-114">Hello 계정에 대 한 hello 구독을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="908a2-115">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="908a2-116">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-116">Create a resource group.</span></span> <span data-ttu-id="908a2-117">기존 리소스 그룹을 사용하는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="908a2-118">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="908a2-119">이 위치는 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="908a2-120">모든 명령을 toocreate 응용 프로그램 게이트웨이 사용 하 여 hello 확인 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="908a2-121">리소스 그룹이 만들었습니다 앞 예제는 hello, **appgw RG** 위치에 **West US**합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="908a2-122">가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="908a2-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="908a2-123">hello 다음 예제에서는 가상 네트워크와 hello 응용 프로그램 게이트웨이 서브넷</span><span class="sxs-lookup"><span data-stu-id="908a2-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="908a2-124">응용 프로그램 게이트웨이에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="908a2-125">이러한 이유로 응용 프로그램 게이트웨이 hello에 대 한 작성 hello 서브넷의 다른 서브넷 toobe 생성 및 사용에 대 한 hello VNET tooallow hello 주소 공간 보다 작아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="908a2-126">Hello 프런트 엔드 구성에 대 한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="908a2-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="908a2-127">공용 IP 리소스 만들기 **publicIP01** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="908a2-128">이 예제에서는 hello hello 응용 프로그램 게이트웨이 프런트 엔드 IP 주소에 대해 공용 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="908a2-129">응용 프로그램 게이트웨이 필요 hello 공용 IP 주소 toohave 동적으로 생성된 된 DNS 이름을 따라서 hello `-DomainNameLabel` hello hello 공용 IP 주소를 만드는 동안 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="908a2-130">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="908a2-130">Create an application gateway</span></span>

<span data-ttu-id="908a2-131">Hello 응용 프로그램 게이트웨이 만들기 전에 모든 구성 항목을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="908a2-132">hello 다음 예제에서는 hello 응용 프로그램 게이트웨이 리소스에 필요한 구성 항목</span><span class="sxs-lookup"><span data-stu-id="908a2-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="908a2-133">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="908a2-133">**Component**</span></span> | <span data-ttu-id="908a2-134">**설명**</span><span class="sxs-lookup"><span data-stu-id="908a2-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="908a2-135">**게이트웨이 IP 구성**</span><span class="sxs-lookup"><span data-stu-id="908a2-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="908a2-136">응용 프로그램 게이트웨이에 대한 IP 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="908a2-137">**백 엔드 풀**</span><span class="sxs-lookup"><span data-stu-id="908a2-137">**Backend pool**</span></span> | <span data-ttu-id="908a2-138">IP 주소, FQDN 또는 hello 웹 응용 프로그램을 호스트 하는 toohello 응용 프로그램 서버에 있는 Nic의 풀</span><span class="sxs-lookup"><span data-stu-id="908a2-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="908a2-139">**상태 프로브**</span><span class="sxs-lookup"><span data-stu-id="908a2-139">**Health probe**</span></span> | <span data-ttu-id="908a2-140">Hello 백 엔드 풀 멤버의 toomonitor hello 상태를 사용 하는 사용자 지정 프로브</span><span class="sxs-lookup"><span data-stu-id="908a2-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="908a2-141">**HTTP 설정**</span><span class="sxs-lookup"><span data-stu-id="908a2-141">**HTTP settings**</span></span> | <span data-ttu-id="908a2-142">포트, 프로토콜, 쿠키 기반 선호도, 프로브 및 시간 제한을 포함한 설정의 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="908a2-143">이러한 설정은 방법을 결정 트래픽 라우팅된 toohello 백 엔드 풀 멤버</span><span class="sxs-lookup"><span data-stu-id="908a2-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="908a2-144">**프런트 엔드 포트**</span><span class="sxs-lookup"><span data-stu-id="908a2-144">**Frontend port**</span></span> | <span data-ttu-id="908a2-145">응용 프로그램 게이트웨이 hello hello 포트에서의 트래픽을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="908a2-146">**수신기**</span><span class="sxs-lookup"><span data-stu-id="908a2-146">**Listener**</span></span> | <span data-ttu-id="908a2-147">프로토콜, 프론트 엔드 IP 구성 및 프론트 엔드 포트의 조합이며,</span><span class="sxs-lookup"><span data-stu-id="908a2-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="908a2-148">들어오는 요청을 수신 대기하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="908a2-149">**규칙**</span><span class="sxs-lookup"><span data-stu-id="908a2-149">**Rule**</span></span>| <span data-ttu-id="908a2-150">경로 hello 트래픽 toohello 적절 한 백 엔드 HTTP 설정에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="908a2-151">프로브 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="908a2-152">hello 다음 코드 조각 프로브 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="908a2-153">기존 응용 프로그램 게이트웨이에서 프로브 제거</span><span class="sxs-lookup"><span data-stu-id="908a2-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="908a2-154">다음 코드 조각 hello에서 기존 응용 프로그램 게이트웨이 프로브를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="908a2-155">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="908a2-155">Get application gateway DNS name</span></span>

<span data-ttu-id="908a2-156">Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="908a2-157">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="908a2-158">tooensure 최종 사용자가 CNAME 레코드를 사용할 수는 hello 응용 프로그램 게이트웨이 적중할 수의 응용 프로그램 게이트웨이 hello toopoint toohello 공용 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="908a2-159">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="908a2-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="908a2-160">toodo hello 응용 프로그램 게이트웨이 및 연결 된 해당 IP/DNS 이름 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여이 검색 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="908a2-161">hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="908a2-162">A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="908a2-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="908a2-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="908a2-163">Next steps</span></span>

<span data-ttu-id="908a2-164">Tooconfigure 방문 하 여 SSL 오프 로딩 자세한: [SSL 오프 로드 구성](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="908a2-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

