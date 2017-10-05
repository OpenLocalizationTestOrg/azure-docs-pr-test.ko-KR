---
title: "내부 부하 분산 장치에서 Azure Application Gateway 사용 | Microsoft Docs"
description: "이 페이지에서는 내부 부하 분산된 끝점이 있는 Azure 응용 프로그램 게이트웨이를 구성하는 지침을 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="a0420-103">내부 부하 분산 장치 (ILB)를 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="a0420-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0420-104">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0420-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="a0420-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0420-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="a0420-106">응용 프로그램 게이트웨이는 인터넷 연결 가상 IP 또는 ILB(내부 부하 분산 장치) 끝점이라고 알려진 인터넷에 노출되지 않은 내부 끝점을 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="a0420-107">ILB를 사용하여 게이트웨이를 구성하는 것은 인터넷에 노출되지 않은 내부 LOB(기간 업무) 응용 프로그램에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="a0420-108">또한 인터넷에 노출되지 않은 보안 경계에 있는 다중 계층이 포함된 서비스/계층에 유용하지만 여전히 라운드 로빈 부하 분산, 세션 인력 또는 SSL 종료가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="a0420-109">이 문서에서는 ILB와 응용 프로그램 게이트웨이를 구성하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a0420-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a0420-110">Before you begin</span></span>

1. <span data-ttu-id="a0420-111">웹 플랫폼 설치 관리자를 사용하여 최신 버전의 Azure PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="a0420-112">**다운로드 페이지** 의 [Windows PowerShell](https://azure.microsoft.com/downloads/)섹션에서 최신 버전을 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="a0420-113">유효한 서브넷과 작업 가상 네트워크가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="a0420-114">가상 네트워크 또는 할당된 공용 IP/VIP와 백엔드 서버가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="a0420-115">응용 프로그램 게이트웨이를 만들려면 나열된 순서로 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="a0420-116">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="a0420-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="a0420-117">게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="a0420-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="a0420-118">게이트웨이 구성 설정</span><span class="sxs-lookup"><span data-stu-id="a0420-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="a0420-119">게이트웨이 시작</span><span class="sxs-lookup"><span data-stu-id="a0420-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="a0420-120">게이트웨이를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="a0420-121">응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-121">Create an application gateway:</span></span>

<span data-ttu-id="a0420-122">**게이트웨이를 생성하려면** `New-AzureApplicationGateway` cmdlet을 사용하여 해당 값을 원하는 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="a0420-123">게이트웨이에 대한 청구는 이 지점에서 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="a0420-124">게이트웨이가 성공적으로 작동되면, 요금청구가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="a0420-125">생성된 게이트웨이의 **유효성을 검사**하려면 `Get-AzureApplicationGateway` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="a0420-126">이 샘플에서 *Description*, *InstanceCount* 및 *GatewaySize*는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="a0420-127">*InstanceCount* 의 기본값은 2이고, 최대값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="a0420-128">*GatewaySize* 에 대한 기본값은 보통입니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="a0420-129">크고 작은 다른 사용 가능한 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-129">Small and Large are other available values.</span></span> <span data-ttu-id="a0420-130">게이트웨이가 아직 시작되지 않았으므로 *Vip* 및 *DnsName*이 빈 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="a0420-131">이 값들은 게이트웨이가 실행 상태가 되면 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-131">These are created once the gateway is in the running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-the-gateway"></a><span data-ttu-id="a0420-132">게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="a0420-132">Configure the gateway</span></span>
<span data-ttu-id="a0420-133">응용 프로그램 게이트웨이는 여러 값으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="a0420-134">값은 연결되어 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="a0420-135">값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-135">The values are:</span></span>

* <span data-ttu-id="a0420-136">**백엔드 서버 풀:** 백엔드 서버 IP 주소의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="a0420-137">나열 된 IP 주소는 VNet 서브넷에 속해야 하거나 또는 공용 IP/VIP 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="a0420-138">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="a0420-139">이러한 설정은 풀에 연결 및 풀 내의 모든 서버에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="a0420-140">**프런트엔드 포트:** 이 포트는 응용 프로그램 게이트웨이에서 열린 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="a0420-141">트래픽이 이 포트에 도달하면, 백엔드 서버 중의 하나가 리디렉트됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="a0420-142">**수신기:** 수신기는 프런트엔드 포트, 프로토콜(Http 또는 Https, 이 경우 대/소문자 구분) 및 SSL 인증서 이름(SSL을 구성하는 작업에 오프로드하는 경우)을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="a0420-143">**규칙:** 규칙은 수신기와 백 엔드 서버 풀을 바인딩하고 특정 수신기에 도달했을 때 트래픽이 이동되는 백 엔드 서버 풀을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="a0420-144">현재는 *기본* 규칙만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="a0420-145">*기본* 규칙은 라운드 로빈 부하 분산입니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="a0420-146">구성 개체를 만들거나, 구성 XML 파일을 사용하여 구성을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="a0420-147">구성 XML 파일을 사용하여 구성을 생성하려면 아래 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="a0420-148">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="a0420-148">Note the following:</span></span>

* <span data-ttu-id="a0420-149">*FrontendIPConfigurations* 요소는 ILB를 사용하여 응용 프로그램 게이트웨이를 구성하는 것에 대한 ILB 세부 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="a0420-150">프런트 엔드 IP *형식* 은 '개인'으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="a0420-151">*StaticIPAddress* 는 게이트웨이가 트래픽을 수신할 내부 IP로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="a0420-152">*StaticIPAddress* 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="a0420-153">설정하지 않은 경우, 서브넷에 배포된 사용 가능한 내부 IP가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="a0420-154">*FrontendIPConfiguration*에 지정된 *이름* 요소 값은 Frontend IPConfiguration을 참조하는 HTTP 수신기의 *FrontendIP* 요소로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="a0420-155">**구성 XML 샘플**</span><span class="sxs-lookup"><span data-stu-id="a0420-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="a0420-156">게이트웨이 구성 설정</span><span class="sxs-lookup"><span data-stu-id="a0420-156">Set the gateway configuration</span></span>
<span data-ttu-id="a0420-157">다음으로, 응용 프로그램 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="a0420-158">`Set-AzureApplicationGatewayConfig` cmdlet을 구성 XML 파일 또는 구성 개체와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-the-gateway"></a><span data-ttu-id="a0420-159">게이트웨이 시작</span><span class="sxs-lookup"><span data-stu-id="a0420-159">Start the gateway</span></span>

<span data-ttu-id="a0420-160">게이트웨이가 구성되면, `Start-AzureApplicationGateway` cmdlet을 사용하여 게이트웨이를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="a0420-161">응용 프로그램 게이트웨이에 대한 청구는 게이트웨이가 성공적으로 작동된 후 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="a0420-162">`Start-AzureApplicationGateway` cmdlet을 완료하려면 최대 15-20분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="a0420-163">게이트웨이 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-163">Verify the gateway status</span></span>

<span data-ttu-id="a0420-164">`Get-AzureApplicationGateway` cmdlet을 사용하여 게이트웨이의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="a0420-165">`Start-AzureApplicationGateway`가 이전 단계에서 성공한 경우 *상태*가 실행 중이어야 하고, Vip와 DnsName에 유효한 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="a0420-166">이 출력 다음 샘플에서는 첫 줄에 cmdlet을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="a0420-167">이 샘플에서 게이트웨이가 실행되며 트래픽을 받을 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="a0420-168">응용 프로그램 게이트웨이는 이 예에서 구성된 ILB 끝점인 10.0.0.10에서 트래픽을 허용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0420-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="a0420-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0420-169">Next steps</span></span>
<span data-ttu-id="a0420-170">보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:</span><span class="sxs-lookup"><span data-stu-id="a0420-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="a0420-171">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="a0420-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="a0420-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="a0420-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

