---
title: "Azure Application Gateway에서 종단 간 SSL 구성 | Microsoft Docs"
description: "이 문서에서는 Azure Resource Manager PowerShell을 사용하여 Application Gateway로 종단 간 SSL을 구성하는 방법에 대해 설명합니다."
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="387f9-103">PowerShell을 사용하여 Application Gateway에서 종단 간 SSL 구성</span><span class="sxs-lookup"><span data-stu-id="387f9-103">Configure end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="387f9-104">개요</span><span class="sxs-lookup"><span data-stu-id="387f9-104">Overview</span></span>

<span data-ttu-id="387f9-105">Application Gateway는 트래픽의 종단 간 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="387f9-106">Application Gateway는 이를 위해 응용 프로그램 게이트웨이에서 SSL 연결을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="387f9-107">그러면 게이트웨이에서 트래픽에 라우팅 규칙을 적용하고, 패킷을 다시 암호화하고, 정의된 라우팅 규칙에 따라 적절한 백 엔드에 패킷을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="387f9-108">웹 서버의 모든 응답은 동일한 프로세스를 거쳐 최종 사용자에게 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="387f9-109">Application Gateway가 사용자 지정 SSL 옵션을 정의하도록 지원하는 다른 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="387f9-110">Application Gateway는 **TLSv1.0**, **TLSv1.1** 및 **TLSv1.2**와 같은 프로토콜 버전을 사용하지 않고 사용할 암호 그룹 및 기본 설정의 순서를 정의하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining the which cipher suites to use and the order of preference.</span></span>  <span data-ttu-id="387f9-111">구성 가능한 SSL 옵션에 대한 자세한 내용은 [SSL 정책 개요](application-gateway-SSL-policy-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="387f9-111">To learn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="387f9-112">SSL 2.0 및 SSL 3.0은 기본적으로 사용할 수 없도록 설정되며 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="387f9-113">보안되지 않은 것으로 간주되며 Application Gateway와 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-113">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![시나리오 이미지][scenario]

## <a name="scenario"></a><span data-ttu-id="387f9-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="387f9-115">Scenario</span></span>

<span data-ttu-id="387f9-116">이 시나리오에서는 PowerShell을 사용하여 종단 간 SSL을 사용하는 Application Gateway를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-116">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="387f9-117">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-117">This scenario will:</span></span>

* <span data-ttu-id="387f9-118">**appgw-rg**라는 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="387f9-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="387f9-119">주소 공간이 10.0.0.0/16인 **appgwvnet**이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="387f9-120">**appgwsubnet** 및 **appsubnet**라는 두 개의 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="387f9-121">SSL 프로토콜 버전 및 암호 그룹을 제한하는 종단 간 SSL 암호화를 지원하는 소형 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-121">Create a small application gateway supporting end to end SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="387f9-122">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="387f9-122">Before you begin</span></span>

<span data-ttu-id="387f9-123">Application Gateway를 사용하여 종단 간 SSL을 구성하려면 게이트웨이에 사용할 인증서와 백 엔드 서버에 사용할 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-123">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="387f9-124">게이트웨이 인증서는 SSL을 사용하여 전송되는 트래픽을 암호화하고 해독하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-124">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="387f9-125">게이트웨이 인증서는 개인 정보 교환(pfx) 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-125">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="387f9-126">이 파일 형식을 사용하면 응용 프로그램 게이트웨이에서 트래픽의 암호화 및 암호 해독을 수행하는 데 필요한 개인 키를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-126">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="387f9-127">종단 간 SSL 암호화의 경우 백 엔드가 Application Gateway를 통해 허용 목록에 추가되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-127">For end to end SSL encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="387f9-128">이 작업은 백 엔드의 공개 인증서를 Application Gateway에 업로드하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-128">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="387f9-129">이렇게 하면 Application Gateway가 알려진 백 엔드 인스턴스하고만 통신하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-129">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="387f9-130">그러면 종단 간 통신의 보안이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-130">This further secures the end to end communication.</span></span>

<span data-ttu-id="387f9-131">이 프로세스는 다음 단계에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-131">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="387f9-132">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="387f9-132">Create the Resource Group</span></span>

<span data-ttu-id="387f9-133">이 섹션에서는 Application Gateway를 포함하는 리소스 그룹을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-133">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="387f9-134">1단계</span><span class="sxs-lookup"><span data-stu-id="387f9-134">Step 1</span></span>

<span data-ttu-id="387f9-135">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-135">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="387f9-136">2단계</span><span class="sxs-lookup"><span data-stu-id="387f9-136">Step 2</span></span>

<span data-ttu-id="387f9-137">이 시나리오에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-137">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="387f9-138">3단계</span><span class="sxs-lookup"><span data-stu-id="387f9-138">Step 3</span></span>

<span data-ttu-id="387f9-139">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="387f9-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="387f9-140">응용 프로그램 게이트웨이에 대한 가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="387f9-140">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="387f9-141">다음 예제에서는 가상 네트워크 및 두 개의 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-141">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="387f9-142">하나의 서브넷은 Application Gateway를 보관하는 데 사용되고</span><span class="sxs-lookup"><span data-stu-id="387f9-142">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="387f9-143">다른 서브넷은 웹 응용 프로그램을 호스트하는 백 엔드 서버에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-143">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="387f9-144">1단계</span><span class="sxs-lookup"><span data-stu-id="387f9-144">Step 1</span></span>

<span data-ttu-id="387f9-145">Application Gateway 자체에 사용할 서브넷의 주소 범위를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-145">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="387f9-146">Application Gateway를 구성하는 서브넷은 크기가 적절해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="387f9-147">Application Gateway는 최대 10개의 인스턴스로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-147">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="387f9-148">각 인스턴스는 서브넷에서 1개의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-148">Each instance takes one IP address from the subnet.</span></span> <span data-ttu-id="387f9-149">서브넷이 너무 적으면 Application Gateway의 크기에 불리한 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="387f9-150">2단계</span><span class="sxs-lookup"><span data-stu-id="387f9-150">Step 2</span></span>

<span data-ttu-id="387f9-151">백 엔드 주소 풀에 사용할 주소 범위를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-151">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="387f9-152">3단계</span><span class="sxs-lookup"><span data-stu-id="387f9-152">Step 3</span></span>

<span data-ttu-id="387f9-153">이전 단계에서 정의한 서브넷을 사용하여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-153">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="387f9-154">4단계</span><span class="sxs-lookup"><span data-stu-id="387f9-154">Step 4</span></span>

<span data-ttu-id="387f9-155">다음 단계에 사용할 가상 네트워크 리소스와 서브넷 리소스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-155">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="387f9-156">프런트 엔드 구성에 대한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="387f9-156">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="387f9-157">Application Gateway에 사용할 공용 IP 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-157">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="387f9-158">이 공용 IP 주소는 다음 단계에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="387f9-159">Application Gateway는 정의된 도메인 레이블로 만든 공용 IP 주소의 사용을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-159">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="387f9-160">도메인 레이블이 동적으로 생성된 공용 IP 주소만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="387f9-161">Application Gateway에 친숙한 DNS 이름이 필요한 경우 CNAME 레코드를 별칭으로 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-161">If you require a friendly dns name for the application gateway, it is recommended to use a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="387f9-162">응용 프로그램 게이트웨이 구성 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="387f9-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="387f9-163">Application Gateway를 만들기 전에 모든 구성 항목을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-163">All configuration items are set before creating the application gateway.</span></span> <span data-ttu-id="387f9-164">다음 단계 응용 프로그램 게이트웨이 리소스에 필요한 구성 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-164">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="387f9-165">1단계</span><span class="sxs-lookup"><span data-stu-id="387f9-165">Step 1</span></span>

<span data-ttu-id="387f9-166">Application Gateway IP 구성을 만듭니다. 이 설정은 Application Gateway에서 사용하는 서브넷을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-166">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="387f9-167">Application Gateway는 시작되면 구성된 서브넷에서 IP 주소를 선택하고 백 엔드 IP 풀의 IP 주소로 네트워크 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-167">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="387f9-168">인스턴스마다 하나의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="387f9-169">2단계</span><span class="sxs-lookup"><span data-stu-id="387f9-169">Step 2</span></span>

<span data-ttu-id="387f9-170">프런트 엔드 IP 구성을 만듭니다. 이 설정은 개인 또는 공용 IP 주소를 Application Gateway의 프런트 엔드에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-170">Create a front-end IP configuration, this setting maps a private or public ip address to the front end of the application gateway.</span></span> <span data-ttu-id="387f9-171">다음 단계는 이전 단계의 공용 IP 주소를 프런트 엔드 IP 구성과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-171">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="387f9-172">3단계</span><span class="sxs-lookup"><span data-stu-id="387f9-172">Step 3</span></span>

<span data-ttu-id="387f9-173">백 엔드 웹 서버의 IP 주소를 사용하여 백 엔드 IP 주소 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-173">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="387f9-174">이러한 IP 주소는 프런트 엔드 IP 끝점에서 들어오는 네트워크 트래픽을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-174">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="387f9-175">사용자 고유의 응용 프로그램 IP 주소 끝점을 추가하려면 다음 IP 주소를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-175">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="387f9-176">정규화된 도메인 이름(FQDN) 역시 -BackendFqdns 스위치를 사용하여 백 엔드 서버의 IP 주소를 대체할 수 있는 유효한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="387f9-177">4단계</span><span class="sxs-lookup"><span data-stu-id="387f9-177">Step 4</span></span>

<span data-ttu-id="387f9-178">공용 IP 끝점에 대한 프런트 엔드 IP 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-178">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="387f9-179">이 포트는 최종 사용자가 연결하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-179">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="387f9-180">5단계</span><span class="sxs-lookup"><span data-stu-id="387f9-180">Step 5</span></span>

<span data-ttu-id="387f9-181">Application Gateway에 대한 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-181">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="387f9-182">이 인증서는 Application Gateway의 트래픽을 암호화하고 해독하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-182">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="387f9-183">이 샘플은 SSL 연결에 사용된 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-183">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="387f9-184">인증서는 .pfx 형식으로 4~12자 사이의 암호이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-184">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="387f9-185">6단계</span><span class="sxs-lookup"><span data-stu-id="387f9-185">Step 6</span></span>

<span data-ttu-id="387f9-186">Application Gateway에 대한 HTTP 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-186">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="387f9-187">사용할 프런트 엔드 IP 구성, 포트 및 SSL 인증서를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-187">Assign the front-end ip configuration, port, and SSL certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="387f9-188">7단계</span><span class="sxs-lookup"><span data-stu-id="387f9-188">Step 7</span></span>

<span data-ttu-id="387f9-189">SSL이 활성화된 백 엔드 풀 리소스에 사용할 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-189">Upload the certificate to be used on the SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="387f9-190">기본 프로브는 공용 키를 백엔드의 IP 주소에 바인딩된 **기본** SSL에서 가져오고 프로브가 받는 공용 키 값과 여기서 사용자가 제공한 공용 키 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-190">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="387f9-191">검색된 공용 키는 사용자가 호스트 헤더 및 SNI를 사용하는 **경우** 트래픽이 이동하는 대상 사이트에 반드시 존재하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-191">The retrieved public key may not necessarily be the intended site to which traffic flows **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="387f9-192">확실하지 않은 경우 백엔드에서 https://127.0.0.1/을 방문하여 **기본** SSL 바인딩에 사용되는 인증서를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="387f9-192">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="387f9-193">이 섹션에서는 해당 요청에서 공개 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-193">Use the public key from that request in this section.</span></span> <span data-ttu-id="387f9-194">호스트 헤더 및 HTTPS의 SNI를 사용하고, 수동 브라우저 요청에서 https://127.0.0.1/로 응답 및 인증서를 받지 않은 경우 백엔드에서 기본 SSL 바인딩을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="387f9-195">그렇게 하지 않으면 프로브가 실패하고 백 엔드가 허용 목록에 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-195">If you do not do so, probes fail and the back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="387f9-196">이 단계에서 제공하는 인증서는 백 엔드에 있는 pfx 인증서의 공개 키이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-196">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="387f9-197">백 엔드 서버에 설치된 인증서(루트 인증서 제외)를 .CER 서식으로 내보내고 이 단계에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-197">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="387f9-198">이 단계에서는 Application Gateway를 통해 백 엔드를 허용 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-198">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="387f9-199">8단계</span><span class="sxs-lookup"><span data-stu-id="387f9-199">Step 8</span></span>

<span data-ttu-id="387f9-200">Application Gateway 백 엔드 http 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-200">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="387f9-201">이전 단계에서 업로드한 인증서를 http 설정에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-201">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="387f9-202">9단계</span><span class="sxs-lookup"><span data-stu-id="387f9-202">Step 9</span></span>

<span data-ttu-id="387f9-203">부하 분산 장치 동작을 구성하는 부하 분산 장치 라우팅 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-203">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="387f9-204">이 예제에서는 기본 라운드 로빈 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="387f9-205">10단계</span><span class="sxs-lookup"><span data-stu-id="387f9-205">Step 10</span></span>

<span data-ttu-id="387f9-206">응용 프로그램 게이트웨이의 인스턴스 크기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-206">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="387f9-207">사용 가능한 크기는 **Standard\_Small**, **Standard\_Medium** 및 **Standard\_Large**입니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-207">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="387f9-208">용량의 경우 사용 가능한 값은 1부터 10까지입니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-208">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="387f9-209">테스트 목적으로 인스턴스 수 1을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="387f9-210">그러나 두 개 미만의 인스턴스 수는 SLA에서 다루지 않으므로 권장되지 않는다는 점을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-210">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="387f9-211">작은 게이트웨이는 개발 테스트용이며 프로덕션용으로는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-211">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="387f9-212">11단계</span><span class="sxs-lookup"><span data-stu-id="387f9-212">Step 11</span></span>

<span data-ttu-id="387f9-213">Application Gateway에서 사용할 SSL 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-213">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="387f9-214">Application Gateway는 SSL 프로토콜 버전에 최소 버전을 설정하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-214">Application Gateway supports the ability to set a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="387f9-215">다음 값은 정의될 수 있는 프로토콜 버전 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-215">The following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="387f9-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="387f9-216">**TLSv1_0**</span></span>
* <span data-ttu-id="387f9-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="387f9-217">**TLSv1_1**</span></span>
* <span data-ttu-id="387f9-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="387f9-218">**TLSv1_2**</span></span>

<span data-ttu-id="387f9-219">최소 프로토콜 버전을 **TLSv1_2**로 설정하고 **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** 및 **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**만 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-219">Sets the minimum protocol version to **TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="387f9-220">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="387f9-220">Create the Application Gateway</span></span>

<span data-ttu-id="387f9-221">위의 모든 단계를 사용하여 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-221">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="387f9-222">게이트웨이 만들기는 긴 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-222">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="387f9-223">기존 Application Gateway의 SSL 프로토콜 버전 제한</span><span class="sxs-lookup"><span data-stu-id="387f9-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="387f9-224">이전 단계에서는 종단 간 SSL을 사용하여 응용 프로그램을 만들고 특정 SSL 프로토콜 버전을 비활성화했습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-224">The preceding steps take you through creating an application with end to end SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="387f9-225">다음 예제에서는 기존 Application Gateway의 특정 SSL 정책을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-225">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="387f9-226">1단계</span><span class="sxs-lookup"><span data-stu-id="387f9-226">Step 1</span></span>

<span data-ttu-id="387f9-227">업데이트할 Application Gateway를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-227">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="387f9-228">2단계</span><span class="sxs-lookup"><span data-stu-id="387f9-228">Step 2</span></span>

<span data-ttu-id="387f9-229">SSL 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-229">Define an SSL policy.</span></span> <span data-ttu-id="387f9-230">다음 예제에서 TLSv1.0 및 TLSv1.1은 비활성화하고 암호 그룹 **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384** 및 **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-230">In the following example, TLSv1.0 and TLSv1.1 are disabled and the cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are the only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="387f9-231">3단계</span><span class="sxs-lookup"><span data-stu-id="387f9-231">Step 3</span></span>

<span data-ttu-id="387f9-232">마지막으로 게이트웨이를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-232">Finally, update the gateway.</span></span> <span data-ttu-id="387f9-233">이 마지막 단계는 오래 걸리는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-233">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="387f9-234">작업이 완료되면 Application Gateway에 종단 간 SSL이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-234">When it is done, end to end SSL is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="387f9-235">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="387f9-235">Get application gateway DNS name</span></span>

<span data-ttu-id="387f9-236">게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-236">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="387f9-237">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="387f9-238">최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-238">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="387f9-239">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="387f9-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="387f9-240">이 작업을 수행하려면 Application Gateway에 연결된 PublicIPAddress 요소를 사용하여 Application Gateway 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-240">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="387f9-241">응용 프로그램 게이트웨이의 DNS 이름은 두 개의 웹 응용 프로그램을 이 DNS 이름으로 가리키는 CNAME 레코드를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-241">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="387f9-242">A 레코드를 사용할 경우 응용 프로그램 게이트웨이 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="387f9-242">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="387f9-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="387f9-243">Next steps</span></span>

<span data-ttu-id="387f9-244">[웹 응용 프로그램 방화벽 개요](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="387f9-244">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
