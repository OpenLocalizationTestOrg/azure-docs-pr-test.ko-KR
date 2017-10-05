---
title: "SSL 오프로드 구성 - Azure Application Gateway - PowerShell | Microsoft Docs"
description: "이 페이지에서는 Azure Resource Manager를 사용하여 SSL 오프로드와 함께 응용 프로그램 게이트웨이를 만드는 지침을 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="5ec9f-103">Azure Resource Manager를 사용하여 SSL 오프로드에 대한 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="5ec9f-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ec9f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5ec9f-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="5ec9f-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ec9f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="5ec9f-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ec9f-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="5ec9f-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5ec9f-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="5ec9f-108">Azure Application Gateway 구성을 사용하여 웹 팜에서 발생하는 비용이 많이 드는 SSL(Secure Sockets Layer) 암호 해독 작업을 방지하기 위한 게이트웨이에서 SSL 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="5ec9f-109">SSL 오프로드는 또한 프런트 엔드 서버 설치 및 웹 응용 프로그램의 관리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5ec9f-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5ec9f-110">Before you begin</span></span>

1. <span data-ttu-id="5ec9f-111">웹 플랫폼 설치 관리자를 사용하는 Azure PowerShell cmdlet의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="5ec9f-112">**다운로드 페이지** 의 [Windows PowerShell](https://azure.microsoft.com/downloads/)섹션에서 최신 버전을 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="5ec9f-113">응용 프로그램 게이트웨이에 대한 가상 네트워크 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-113">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="5ec9f-114">서브넷을 사용 중인 가상 컴퓨터 또는 클라우드 배포가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="5ec9f-115">응용 프로그램 게이트웨이는 가상 네트워크 서브넷에서 단독이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="5ec9f-116">응용 프로그램 게이트웨이를 사용하도록 구성된 서버가 존재하거나 가상 네트워크나 공용 IP/VIP가 할당된 해당 끝점이 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-116">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="5ec9f-117">응용 프로그램 게이트웨이를 만드는 데 필요한 것은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5ec9f-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="5ec9f-118">**백 엔드 서버 풀:** 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="5ec9f-119">나열된 IP 주소는 가상 네트워크 서브넷에 속하거나 공용 IP/VIP이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-119">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="5ec9f-120">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="5ec9f-121">이러한 설정은 풀에 연결 및 풀 내의 모든 서버에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="5ec9f-122">**프런트 엔드 포트:** 이 포트는 응용 프로그램 게이트웨이에 열려 있는 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="5ec9f-123">트래픽이 이 포트에 도달하면, 백 엔드 서버 중의 하나로 리디렉트됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="5ec9f-124">**수신기:** 수신기에는 프런트 엔드 포트, 프로토콜(Http 또는 Https, 대/소문자 구분) 및 SSL 인증서 이름(SSL 오프로드를 구성하는 경우)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="5ec9f-125">**규칙:** 규칙은 수신기와 백 엔드 서버 풀을 바인딩하고 특정 수신기에 도달했을 때 트래픽이 이동되는 백 엔드 서버 풀을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="5ec9f-126">현재는 *기본* 규칙만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="5ec9f-127">*기본* 규칙은 라운드 로빈 부하 분산입니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-127">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="5ec9f-128">**추가 구성 정보**</span><span class="sxs-lookup"><span data-stu-id="5ec9f-128">**Additional configuration notes**</span></span>

<span data-ttu-id="5ec9f-129">SSL 인증서 구성에서 **HttpListener** 의 프로토콜은 *Https* (대/소문자 구분)로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-129">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="5ec9f-130">**SslCertificate** 요소는 SSL 인증서에 대해 구성된 변수 값과 함께 **HttpListener**에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-130">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="5ec9f-131">프런트 엔드 포트는 443으로 업데이트되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-131">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="5ec9f-132">**쿠키 기반 선호도를 사용하도록 설정**: 응용 프로그램 게이트웨이는 클라이언트 세션의 요청이 항상 웹 팜에 있는 동일한 VM으로 전송되도록 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-132">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="5ec9f-133">게이트웨이에서 트래픽을 적절하게 지시할 수 있는 세션 쿠키를 삽입하면 이 시나리오가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-133">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="5ec9f-134">쿠키 기반 선호도를 사용하려면 **BackendHttpSettings** 요소에서 **CookieBasedAffinity**를 *Enabled*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-134">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="5ec9f-135">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-135">Create an application gateway</span></span>

<span data-ttu-id="5ec9f-136">Azure 클래식 배포 모델 및 Azure Resource Manager 간의 차이점은 응용 프로그램 게이트웨이를 만드는 순서와 구성할 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-136">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="5ec9f-137">Resource Manager를 사용하면 응용 프로그램 게이트웨이의 모든 구성 요소가 개별적으로 구성된 후 응용 프로그램 게이트웨이 리소스를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-137">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="5ec9f-138">다음은 응용 프로그램 게이트웨이를 만드는 데 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-138">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="5ec9f-139">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="5ec9f-140">응용 프로그램 게이트웨이에 대한 가상 네트워크, 서브넷 및 공용 IP 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-140">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="5ec9f-141">응용 프로그램 게이트웨이 구성 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="5ec9f-142">응용 프로그램 게이트웨이 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="5ec9f-143">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="5ec9f-144">Azure 리소스 관리자 cmdlet을 사용하려면 PowerShell 모드로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-144">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="5ec9f-145">자세한 내용은 [Resource Manager에서 Windows PowerShell](../powershell-azure-resource-manager.md)사용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="5ec9f-146">1단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="5ec9f-147">2단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-147">Step 2</span></span>

<span data-ttu-id="5ec9f-148">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="5ec9f-149">자격 증명을 사용하여 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-149">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="5ec9f-150">3단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-150">Step 3</span></span>

<span data-ttu-id="5ec9f-151">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-151">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="5ec9f-152">4단계:</span><span class="sxs-lookup"><span data-stu-id="5ec9f-152">Step 4</span></span>

<span data-ttu-id="5ec9f-153">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="5ec9f-154">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="5ec9f-155">이 설정은 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-155">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="5ec9f-156">응용 프로그램 게이트웨이를 만들기 위한 모든 명령이 동일한 리소스 그룹을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-156">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="5ec9f-157">위 예제에서는 **appgw-RG**라는 리소스 그룹과 **미국 서부**라는 위치를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-157">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="5ec9f-158">응용 프로그램 게이트웨이에 대한 가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-158">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="5ec9f-159">다음 예제에서는 Resource Manager를 사용하여 가상 네트워크를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-159">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="5ec9f-160">1단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="5ec9f-161">이 샘플은 주소 범위 10.0.0.0/24를 가상 네트워크를 만드는 데 사용할 서브넷 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-161">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="5ec9f-162">2단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="5ec9f-163">이 샘플은 접두사 10.0.0.0/16과 서브넷 10.0.0.0/24를 사용하여 미국 서부 지역에 리소스 그룹 **appgw-rg**에서 **appgwvnet**이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="5ec9f-164">3단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="5ec9f-165">이 샘플은 다음 단계를 위해 $subnet 변수에 서브넷 개체를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-165">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="5ec9f-166">프런트 엔드 구성에 대한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-166">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="5ec9f-167">이 샘플은 미국 서부 지역에 리소스 그룹 **appgw-rg**에서 공용 IP 리소스 **publicIP01**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="5ec9f-168">응용 프로그램 게이트웨이 구성 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="5ec9f-169">1단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="5ec9f-170">이 샘플은 **gatewayIP01**이라는 Application Gateway IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="5ec9f-171">응용 프로그램 게이트웨이는 시작되면 구성된 서브넷에서 IP 주소를 선택하고 백 엔드 IP 풀의 IP 주소로 네트워크 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-171">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="5ec9f-172">인스턴스마다 하나의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="5ec9f-173">2단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="5ec9f-174">이 샘플은 IP 주소가 **134.170.185.46**, **134.170.188.221**, **134.170.185.50**인 **pool01**이라는 백 엔드 IP 주소 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-174">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="5ec9f-175">이러한 값은 프런트 엔드 IP 끝점에서 들어오는 네트워크 트래픽을 수신하는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-175">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="5ec9f-176">앞의 예제에서 IP 주소를 웹 응용 프로그램 끝점의 IP 주소로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-176">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="5ec9f-177">3단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="5ec9f-178">이 샘플은 백 엔드 풀에서 부하가 분산된 네트워크 트래픽에 대해 Application Gateway 설정 **poolsetting01**을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-178">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="5ec9f-179">4단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="5ec9f-180">이 샘플은 공용 IP 끝점에 대해 **frontendport01**이라는 프런트 엔드 IP 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-180">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="5ec9f-181">5단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="5ec9f-182">이 샘플은 SSL 연결에 사용된 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="5ec9f-183">인증서는 .pfx 형식으로 4~12자 사이의 암호이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="5ec9f-184">6단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="5ec9f-185">이 샘플은 **fipconfig01**이라는 프런트 엔드 IP 구성을 만들고 프런트 엔드 IP 구성에 공용 IP 주소를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-185">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="5ec9f-186">7단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="5ec9f-187">이 샘플은 **listener01**이라는 수신기를 만들고 프런트 엔드 IP 구성 및 인증서에 프런트 엔드 포트를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-187">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="5ec9f-188">8단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="5ec9f-189">이 샘플은 **rule01**이라는 부하 분산 장치 라우팅 규칙을 만들고 부하 분산 장치 동작을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-189">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="5ec9f-190">9단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="5ec9f-191">이 샘플은 응용 프로그램 게이트웨이의 인스턴스 크기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-191">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="5ec9f-192">*InstanceCount* 의 기본값은 2이고, 최대값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-192">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="5ec9f-193">*GatewaySize* 에 대한 기본값은 보통입니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-193">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="5ec9f-194">Standard_Small, Standard_Medium 및 Standard_Large 간에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="5ec9f-195">10단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="5ec9f-196">이 단계는 Application Gateway에서 사용할 SSL 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-196">This step defines the SSL policy to use on the application gateway.</span></span> <span data-ttu-id="5ec9f-197">[Application Gateway에서 SSL 정책 버전 및 암호 그룹 구성](application-gateway-configure-ssl-policy-powershell.md)을 방문하여 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="5ec9f-198">New-AzureApplicationGateway를 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="5ec9f-199">이 샘플은 이전 단계의 모든 구성 항목을 가진 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-199">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="5ec9f-200">이 예제에서는 Application Gateway를 **appgwtest**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-200">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="5ec9f-201">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="5ec9f-201">Get application gateway DNS name</span></span>

<span data-ttu-id="5ec9f-202">게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-202">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="5ec9f-203">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="5ec9f-204">최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-204">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="5ec9f-205">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5ec9f-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="5ec9f-206">이 작업을 수행하려면 Application Gateway에 연결된 PublicIPAddress 요소를 사용하여 Application Gateway 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-206">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="5ec9f-207">응용 프로그램 게이트웨이의 DNS 이름은 두 개의 웹 응용 프로그램을 이 DNS 이름으로 가리키는 CNAME 레코드를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-207">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="5ec9f-208">A 레코드를 사용할 경우 응용 프로그램 게이트웨이 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-208">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="5ec9f-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ec9f-209">Next steps</span></span>

<span data-ttu-id="5ec9f-210">ILB(내부 부하 분산 장치)에서 사용되도록 응용 프로그램 게이트웨이를 구성하려면 [ILB(내부 부하 분산 장치)를 사용하여 응용 프로그램 게이트웨이 만들기](application-gateway-ilb.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ec9f-210">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="5ec9f-211">보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:</span><span class="sxs-lookup"><span data-stu-id="5ec9f-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="5ec9f-212">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="5ec9f-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="5ec9f-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="5ec9f-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

