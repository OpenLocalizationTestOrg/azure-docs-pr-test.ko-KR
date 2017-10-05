---
title: "내부 부하 분산 장치에서 Azure Application Gateway 사용 - PowerShell | Microsoft Docs"
description: "이 페이지에서는 Azure Resource Manager용 ILB(내부 부하 분산 장치)를 사용하여 Azure 응용 프로그램 게이트웨이를 만들고, 구성하고, 시작하고, 삭제하기 위한 지침을 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d218eab7e9f124e4825a8a781b4eeb0dcca58b4a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="ea0ca-103">Azure 리소스 관리자를 사용하여 ILB(내부 부하 분산 장치)에서 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea0ca-104">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea0ca-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="ea0ca-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea0ca-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="ea0ca-106">Azure 응용 프로그램 게이트웨이는 인터넷 연결 VIP 또는 ILB(내부 부하 분산 장치) 끝점이라고 알려진 인터넷에 노출되지 않은 내부 끝점을 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed to the Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="ea0ca-107">ILB를 사용하여 게이트웨이를 구성하는 것은 인터넷에 노출되지 않은 비즈니스 응용 프로그램의 내부 라인에 대해 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-107">Configuring the gateway with an ILB is useful for internal line-of-business applications that are not exposed to the Internet.</span></span> <span data-ttu-id="ea0ca-108">또한 인터넷에 노출되지 않은 보안 경계에 앉아 있는 다중 계층 응용 프로그램 내에 포함된 서비스 및 계층에 유용하지만 여전히 라운드 로빈 부하 분산, 세션 인력 또는 SSL(Secure Sockets Layer) 종료가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed to the Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="ea0ca-109">이 문서는 ILB와 응용 프로그램 게이트웨이 구성 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ea0ca-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ea0ca-110">Before you begin</span></span>

1. <span data-ttu-id="ea0ca-111">웹 플랫폼 설치 관리자를 사용하는 Azure PowerShell cmdlet의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="ea0ca-112">**다운로드 페이지** 의 [Windows PowerShell](https://azure.microsoft.com/downloads/)섹션에서 최신 버전을 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="ea0ca-113">응용 프로그램 게이트웨이에 대한 가상 네트워크 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="ea0ca-114">서브넷을 사용 중인 가상 컴퓨터 또는 클라우드 배포가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="ea0ca-115">응용 프로그램 게이트웨이는 가상 네트워크 서브넷에서 단독이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="ea0ca-116">응용 프로그램 게이트웨이를 사용하도록 구성된 서버가 존재하거나 가상 네트워크나 공용 IP/VIP가 할당된 해당 끝점이 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="ea0ca-117">응용 프로그램 게이트웨이를 만드는 데 필요한 것은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ea0ca-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="ea0ca-118">**백 엔드 서버 풀:** 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="ea0ca-119">나열된 IP 주소는 응용 프로그램 게이트웨이에 대한 다른 서브넷의 가상 네트워크에 속하거나 공용 IP/VIP이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-119">The IP addresses listed should either belong to the virtual network but in a different subnet for the application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="ea0ca-120">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="ea0ca-121">이러한 설정은 풀에 연결 및 풀 내의 모든 서버에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="ea0ca-122">**프런트 엔드 포트:** 이 포트는 응용 프로그램 게이트웨이에 열려 있는 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="ea0ca-123">트래픽이 이 포트에 도달하면, 백 엔드 서버 중의 하나로 리디렉트됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="ea0ca-124">**수신기:** 수신기에는 프런트 엔드 포트, 프로토콜(Http 또는 Https, 이 경우 대/소문자 구분) 및 SSL 인증서 이름(SSL 오프로드를 구성하는 경우)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="ea0ca-125">**규칙:** 규칙은 수신기와 백 엔드 서버 풀을 바인딩하고 특정 수신기에 도달했을 때 트래픽이 이동되는 백 엔드 서버 풀을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="ea0ca-126">현재는 *기본* 규칙만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="ea0ca-127">*기본* 규칙은 라운드 로빈 부하 분산입니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-127">The *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="ea0ca-128">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-128">Create an application gateway</span></span>

<span data-ttu-id="ea0ca-129">Azure Classic 및 Azure Resource Manager 간의 차이점은 응용 프로그램 게이트웨이를 만드는 순서와 구성할 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-129">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>
<span data-ttu-id="ea0ca-130">Resource Manager를 사용하면 응용 프로그램 게이트웨이를 만드는 모든 항목이 개별적으로 구성된 후 응용 프로그램 게이트웨이 리소스를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-130">With Resource Manager, all items that make an application gateway is configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="ea0ca-131">다음은 응용 프로그램 게이트웨이를 만드는 데 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-131">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="ea0ca-132">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="ea0ca-133">응용 프로그램 게이트웨이에 대한 가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-133">Create a virtual network and a subnet for the application gateway</span></span>
3. <span data-ttu-id="ea0ca-134">응용 프로그램 게이트웨이 구성 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="ea0ca-135">응용 프로그램 게이트웨이 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="ea0ca-136">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="ea0ca-137">Azure 리소스 관리자 cmdlet을 사용하려면 PowerShell 모드로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-137">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="ea0ca-138">자세한 내용은 [Resource Manager에서 Windows PowerShell](../powershell-azure-resource-manager.md)사용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="ea0ca-139">1단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="ea0ca-140">2단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-140">Step 2</span></span>

<span data-ttu-id="ea0ca-141">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-141">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="ea0ca-142">자격 증명을 사용하여 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-142">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="ea0ca-143">3단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-143">Step 3</span></span>

<span data-ttu-id="ea0ca-144">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-144">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="ea0ca-145">4단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-145">Step 4</span></span>

<span data-ttu-id="ea0ca-146">새 리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="ea0ca-147">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="ea0ca-148">이 위치는 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-148">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="ea0ca-149">응용 프로그램 게이트웨이를 만들기 위한 모든 명령이 동일한 리소스 그룹을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-149">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="ea0ca-150">이전 예제에서는 "appgw-rg"라는 리소스 그룹과 "미국 서부"라는 위치를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-150">In the preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="ea0ca-151">응용 프로그램 게이트웨이에 대한 가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-151">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="ea0ca-152">다음 예제에서는 Resource Manager를 사용하여 가상 네트워크를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-152">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="ea0ca-153">1단계:</span><span class="sxs-lookup"><span data-stu-id="ea0ca-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="ea0ca-154">이 단계에서는 주소 범위 10.0.0.0/24를 가상 네트워크를 만드는 데 사용할 서브넷 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-154">This step assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="ea0ca-155">2단계:</span><span class="sxs-lookup"><span data-stu-id="ea0ca-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="ea0ca-156">이 단계에서는 접두사 10.0.0.0/16과 서브넷 10.0.0.0/24를 사용하여 미국 서부 지역에 리소스 그룹 "appgw-rg"에서 "appgwvnet"이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="ea0ca-157">3단계:</span><span class="sxs-lookup"><span data-stu-id="ea0ca-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="ea0ca-158">이 단계에서는 다음 단계를 위해 $subnet 변수에 서브넷 개체를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-158">This step assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="ea0ca-159">응용 프로그램 게이트웨이 구성 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="ea0ca-160">1단계:</span><span class="sxs-lookup"><span data-stu-id="ea0ca-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="ea0ca-161">이 단계에서는 "gatewayIP01"이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="ea0ca-162">응용 프로그램 게이트웨이는 시작되면 구성된 서브넷에서 IP 주소를 선택하고 백 엔드 IP 풀의 IP 주소로 네트워크 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-162">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="ea0ca-163">인스턴스마다 하나의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="ea0ca-164">2단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="ea0ca-165">이 단계에서는 IP 주소가 "10.1.1.8, 10.1.1.9, 10.1.1.10"인 "pool01"이라는 백 엔드 IP 주소 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-165">This step configures the back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="ea0ca-166">이러한 IP 주소는 프런트 엔드 IP 끝점에서 들어오는 네트워크 트래픽을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-166">Those are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="ea0ca-167">사용자 고유의 응용 프로그램 IP 주소 끝점을 추가하려면 이전 IP 주소를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-167">You replace the preceding IP addresses to add your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="ea0ca-168">3단계:</span><span class="sxs-lookup"><span data-stu-id="ea0ca-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="ea0ca-169">이 단계에서는 백 엔드 풀에서 부하가 분산된 네트워크 트래픽에 대해 Application Gateway 설정 "poolsetting01"을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-169">This step configures application gateway setting "poolsetting01" for the load balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="ea0ca-170">4단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="ea0ca-171">이 단계에서는 ILB에 대해 "frontendport01"이라는 프런트 엔드 IP 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-171">This step configures the front-end IP port named "frontendport01" for the ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="ea0ca-172">5단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="ea0ca-173">이 단계에서는 "fipconfig01"라는 프런트 엔드 IP 구성을 만들고 현재 가상 네트워크 서브넷의 개인 IP와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-173">This step creates the front-end IP configuration called "fipconfig01" and associates it with a private IP from the current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="ea0ca-174">6단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="ea0ca-175">이 단계에서는 "listener01"라는 수신기를 만들고 프런트 엔드 IP 구성에 프런트 엔드 포트를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-175">This step creates the listener called "listener01" and associates the front-end port to the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="ea0ca-176">7단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="ea0ca-177">이 단계에서는 "rule01"라는 부하 분산 장치 라우팅 규칙을 만들고 부하 분산 장치 동작을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-177">This step creates the load balancer routing rule called "rule01" that configures the load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="ea0ca-178">8단계:</span><span class="sxs-lookup"><span data-stu-id="ea0ca-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="ea0ca-179">이 단계에서는 Application Gateway의 인스턴스 크기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-179">This step configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="ea0ca-180">*InstanceCount* 의 기본값은 2이고, 최대값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-180">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="ea0ca-181">*GatewaySize* 에 대한 기본값은 보통입니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-181">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="ea0ca-182">Standard_Small, Standard_Medium 및 Standard_Large 간에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="ea0ca-183">New-AzureApplicationGateway를 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="ea0ca-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="ea0ca-184">이전 단계의 모든 구성 항목으로 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-184">Creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="ea0ca-185">이 예제에서는 응용 프로그램 게이트웨이를 "appgwtest"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-185">In this example, the application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="ea0ca-186">이 단계에서는 이전 단계의 모든 구성 항목으로 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-186">This step creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="ea0ca-187">이 예제에서는 응용 프로그램 게이트웨이를 "appgwtest"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-187">In the example, the application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="ea0ca-188">응용 프로그램 게이트웨이 삭제</span><span class="sxs-lookup"><span data-stu-id="ea0ca-188">Delete an application gateway</span></span>

<span data-ttu-id="ea0ca-189">Application Gateway를 삭제하려면 다음 단계를 순서대로 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-189">To delete an application gateway, you need to do the following steps in order:</span></span>

1. <span data-ttu-id="ea0ca-190">`Stop-AzureRmApplicationGateway` cmdlet을 사용하여 게이트웨이를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-190">Use the `Stop-AzureRmApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="ea0ca-191">`Remove-AzureRmApplicationGateway` cmdlet을 사용하여 게이트웨이를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-191">Use the `Remove-AzureRmApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="ea0ca-192">`Get-AzureApplicationGateway` cmdlet을 사용하여 게이트웨이가 제거되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-192">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="ea0ca-193">1단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-193">Step 1</span></span>

<span data-ttu-id="ea0ca-194">응용 프로그램 게이트웨이 개체를 가져오고 "$getgw" 변수에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-194">Get the application gateway object and associate it to a variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="ea0ca-195">2단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-195">Step 2</span></span>

<span data-ttu-id="ea0ca-196">`Stop-AzureRmApplicationGateway`를 사용하여 응용 프로그램 게이트웨이를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-196">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span></span> <span data-ttu-id="ea0ca-197">이 샘플의 첫째 줄에는 `Stop-AzureRmApplicationGateway` cmdlet이 표시되고 그 다음에 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-197">This sample shows the `Stop-AzureRmApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="ea0ca-198">응용 프로그램 게이트웨이가 중지됨 상태가 되면 `Remove-AzureRmApplicationGateway` cmdlet을 사용하여 서비스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-198">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="ea0ca-199">**-force** 스위치를 사용하여 제거 확인 메시지가 표시되지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-199">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="ea0ca-200">서비스가 제거되었는지 확인하려면 `Get-AzureRmApplicationGateway` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-200">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="ea0ca-201">이 단계는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="ea0ca-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea0ca-202">Next steps</span></span>

<span data-ttu-id="ea0ca-203">SSL 오프로드를 구성하려는 경우 [SSL 오프로드에 대해 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-203">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="ea0ca-204">ILB에서 사용되도록 응용 프로그램 게이트웨이를 구성하려면 [ILB(내부 부하 분산 장치)를 사용하여 응용 프로그램 게이트웨이 만들기](application-gateway-ilb.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea0ca-204">If you want to configure an application gateway to use with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="ea0ca-205">보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:</span><span class="sxs-lookup"><span data-stu-id="ea0ca-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="ea0ca-206">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="ea0ca-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="ea0ca-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="ea0ca-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

