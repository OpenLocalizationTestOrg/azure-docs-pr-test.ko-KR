---
title: "aaaCreate, 시작 또는 응용 프로그램 게이트웨이 삭제 합니다. | Microsoft Docs"
description: "이 페이지에서는 toocreate, 구성, 시작 및 Azure 응용 프로그램 게이트웨이 삭제 하는 지침을 제공 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="73bcb-103">PowerShell을 사용하여 Application Gateway 만들기, 시작 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="73bcb-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="73bcb-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="73bcb-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="73bcb-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="73bcb-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="73bcb-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="73bcb-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="73bcb-107">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="73bcb-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="73bcb-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="73bcb-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="73bcb-109">Azure Application Gateway는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="73bcb-110">장애 조치의 경우 서로 다른 서버 간에 HTTP 요청 성능 라우팅 hello 클라우드 또는 온-프레미스에 있는지 여부를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="73bcb-111">응용 프로그램 게이트웨이는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타를 포함하여 많은 ADC(Application Delivery Controller)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="73bcb-112">지원 되는 기능의 전체 목록은 toofind 방문 [응용 프로그램 게이트웨이 개요](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="73bcb-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="73bcb-113">이 문서 단계별로 hello 단계 toocreate, 구성, 시작 및 응용 프로그램 게이트웨이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="73bcb-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="73bcb-114">Before you begin</span></span>

1. <span data-ttu-id="73bcb-115">Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="73bcb-116">다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="73bcb-117">기존 가상 네트워크를 사용 하도록 설정한 경우 기존 빈 서브넷을 선택 하거나 hello 응용 프로그램 게이트웨이에서 사용 하기 위해서만 하려면 기존 가상 네트워크에서 새 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="73bcb-118">Hello 응용 프로그램 게이트웨이 tooa 다른 가상 네트워크를 배포할 수 없습니다 hello 리소스 보다 하려는 hello 응용 프로그램 게이트웨이 뒤 toodeploy vnet 피어 링을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="73bcb-119">toolearn 더 방문 [Vnet 피어 링](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="73bcb-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="73bcb-120">유효한 서브넷과 작업 가상 네트워크가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="73bcb-121">가상 컴퓨터 또는 클라우드 배포 없습니다 hello 서브넷 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="73bcb-122">hello 응용 프로그램 게이트웨이 자체 가상 네트워크 서브넷에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="73bcb-123">toouse hello 응용 프로그램 게이트웨이 구성 하는 hello 서버에 존재 해야 하거나 또는 hello 가상 네트워크에서 공용 IP/VIP와 만든 끝점을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="73bcb-124">필요한 toocreate 응용 프로그램 게이트웨이 란?</span><span class="sxs-lookup"><span data-stu-id="73bcb-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="73bcb-125">Hello를 사용 하는 경우 `New-AzureApplicationGateway` 명령 toocreate hello 응용 프로그램 게이트웨이 구성 없이 시점에서 설정 되 고 hello 새로 만든 리소스 구성 된 XML 또는 구성 개체를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="73bcb-126">hello 값은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-126">hello values are:</span></span>

* <span data-ttu-id="73bcb-127">**백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="73bcb-128">나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="73bcb-129">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="73bcb-130">이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="73bcb-131">**프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="73bcb-132">트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="73bcb-133">**수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="73bcb-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="73bcb-134">**규칙:** hello 규칙 hello 수신기 및 hello 백 엔드 서버 풀 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="73bcb-135">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="73bcb-135">Create an application gateway</span></span>

<span data-ttu-id="73bcb-136">응용 프로그램 게이트웨이 toocreate:</span><span class="sxs-lookup"><span data-stu-id="73bcb-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="73bcb-137">응용 프로그램 게이트웨이 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="73bcb-138">구성 XML 파일 또는 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="73bcb-139">새로 만든 응용 프로그램 게이트웨이 리소스 hello 구성 toohello를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="73bcb-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="73bcb-140">응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브 tooconfigure 해야 할 경우 참조 [PowerShell을 사용 하 여 사용자 지정 프로브 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-probe-classic-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="73bcb-141">자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md) 을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![예제 시나리오][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="73bcb-143">응용 프로그램 게이트웨이 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="73bcb-143">Create an application gateway resource</span></span>

<span data-ttu-id="73bcb-144">toocreate hello 게이트웨이 사용 하 여 hello `New-AzureApplicationGateway` cmdlet, 사용자의 정보로 hello 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="73bcb-145">게이트웨이 hello에 대 한 청구가 시점에서 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="73bcb-146">청구는 hello 게이트웨이 성공적으로 시작 하는 경우 이후 단계에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="73bcb-147">hello 다음 만드는 예제 응용 프로그램 게이트웨이 "testvnet1"과 "서브넷-1" 이라는 서브넷 이라는 가상 네트워크를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="73bcb-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="73bcb-148">*Description*, *InstanceCount* 및 *GatewaySize*는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="73bcb-149">게이트웨이 hello toovalidate 만들어진 hello를 사용할 수 있습니다, `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="73bcb-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="73bcb-150">기본값에 대 한 hello *InstanceCount* 최대 값이 10 인 2입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="73bcb-151">에 대 한 기본값을 hello *GatewaySize* 보통입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="73bcb-152">작게, 보통 및 크게를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="73bcb-153">*Virtualip* 및 *DnsName* hello 게이트웨이가 아직 시작 되지 않았습니다. 때문에 출력이 빈 값으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="73bcb-154">Hello 게이트웨이 hello 실행 중 상태에에서 있으면 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="73bcb-155">Hello 응용 프로그램 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-155">Configure hello application gateway</span></span>

<span data-ttu-id="73bcb-156">XML 또는 구성 개체를 사용 하 여 hello 응용 프로그램 게이트웨이 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="73bcb-157">XML을 사용 하 여 hello 응용 프로그램 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="73bcb-158">다음 예제는 hello, 모든 응용 프로그램 게이트웨이 설정 XML 파일 tooconfigure를 사용 하 고 응용 프로그램 게이트웨이 리소스 toohello 커밋하기 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="73bcb-159">1단계</span><span class="sxs-lookup"><span data-stu-id="73bcb-159">Step 1</span></span>

<span data-ttu-id="73bcb-160">다음 텍스트 tooNotepad hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-160">Copy hello following text tooNotepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="73bcb-161">Hello hello 구성 항목에 대 한 hello 괄호 사이 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="73bcb-162">Hello 파일 확장명이.xml으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73bcb-163">Http 또는 Https hello 프로토콜 항목은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="73bcb-164">다음 예제는 hello toouse 구성 파일 tooset hello 응용 프로그램 게이트웨이를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="73bcb-165">hello 예제에서는 로드 된 공용 포트 80의 HTTP 트래픽을 분산 시키고 후 tooback 끝 포트 80에서 두 개의 IP 주소 간의 네트워크 트래픽을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
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

#### <a name="step-2"></a><span data-ttu-id="73bcb-166">2단계</span><span class="sxs-lookup"><span data-stu-id="73bcb-166">Step 2</span></span>

<span data-ttu-id="73bcb-167">다음으로 hello 응용 프로그램 게이트웨이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-167">Next, set hello application gateway.</span></span> <span data-ttu-id="73bcb-168">사용 하 여 hello `Set-AzureApplicationGatewayConfig` 구성 XML 파일을 사용 하 여 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="73bcb-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="73bcb-169">구성 개체를 사용 하 여 hello 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="73bcb-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="73bcb-170">다음 예제는 hello tooconfigure 구성 개체를 사용 하 여 응용 프로그램 게이트웨이 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="73bcb-171">모든 구성 항목을 개별적으로 구성 되며 다음 추가 해야 tooan 응용 프로그램 게이트웨이 구성 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="73bcb-172">Hello를 사용 하면 hello 구성 개체를 만든 후 `Set-AzureApplicationGateway` 명령 toocommit hello 구성 toohello 이전에 응용 프로그램 게이트웨이 리소스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="73bcb-173">값 tooeach 구성 개체를 할당 하기 전에 필요한 toodeclare PowerShell가 어떤 종류의 개체 저장을 위해 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="73bcb-174">hello 첫 번째 toocreate hello 개별 품목 대상을 정의 `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="73bcb-175">1단계</span><span class="sxs-lookup"><span data-stu-id="73bcb-175">Step 1</span></span>

<span data-ttu-id="73bcb-176">모든 개별 구성 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-176">Create all individual configuration items.</span></span>

<span data-ttu-id="73bcb-177">다음 예제는 hello와 같이 hello 프런트 엔드 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="73bcb-178">다음 예제는 hello와 같이 hello 프런트 엔드 포트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="73bcb-179">Hello 백 엔드 서버 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="73bcb-180">Hello 다음 예제와 같이 toohello 백 엔드 서버 풀에 추가 된 hello IP 주소를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="73bcb-181">Hello $server 개체 tooadd hello 값 toohello 백 엔드 풀 개체 ($pool)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="73bcb-182">Hello 백 엔드 서버 풀 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="73bcb-183">Hello 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="73bcb-184">Hello 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="73bcb-185">2단계</span><span class="sxs-lookup"><span data-stu-id="73bcb-185">Step 2</span></span>

<span data-ttu-id="73bcb-186">모든 개별 구성 항목 tooan 응용 프로그램 게이트웨이 구성 개체 ($appgwconfig)를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="73bcb-187">Hello 프런트 엔드 IP toohello 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="73bcb-188">Hello 프런트 엔드 포트 toohello 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="73bcb-189">Hello 백 엔드 서버 풀 toohello 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="73bcb-190">Hello 백 엔드 풀 설정을 toohello 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="73bcb-191">Hello 수신기 toohello 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="73bcb-192">Hello 규칙 toohello 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="73bcb-193">3단계</span><span class="sxs-lookup"><span data-stu-id="73bcb-193">Step 3</span></span>
<span data-ttu-id="73bcb-194">Hello 구성 개체 toohello 응용 프로그램 게이트웨이 리소스를 사용 하 여 커밋 `Set-AzureApplicationGatewayConfig`합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="73bcb-195">Hello 게이트웨이 시작</span><span class="sxs-lookup"><span data-stu-id="73bcb-195">Start hello gateway</span></span>

<span data-ttu-id="73bcb-196">Hello를 사용 하 여 hello 게이트웨이 구성한 후 `Start-AzureApplicationGateway` cmdlet toostart hello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="73bcb-197">응용 프로그램 게이트웨이 대 한 청구 hello 게이트웨이 성공적으로 시작 된 후 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="73bcb-198">hello `Start-AzureApplicationGateway` cmdlet toofinish too15 20 분이 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="73bcb-199">Hello 게이트웨이 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-199">Verify hello gateway status</span></span>

<span data-ttu-id="73bcb-200">사용 하 여 hello `Get-AzureApplicationGateway` hello 게이트웨이의 cmdlet toocheck hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="73bcb-201">경우 `Start-AzureApplicationGateway` hello 이전 단계에서 성공한 *상태* 실행 해야 하 고 *Vip* 및 *DnsName* 유효한 항목 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="73bcb-202">hello 다음 예제에서는 최대, 실행 되는 응용 프로그램 게이트웨이 및 대상이 지정 되었으며 준비 tootake 트래픽 `http://<generated-dns-name>.cloudapp.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

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
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="73bcb-203">Hello 응용 프로그램 게이트웨이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-203">Delete hello application gateway</span></span>

<span data-ttu-id="73bcb-204">toodelete hello 응용 프로그램 게이트웨이:</span><span class="sxs-lookup"><span data-stu-id="73bcb-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="73bcb-205">사용 하 여 hello `Stop-AzureApplicationGateway` cmdlet toostop hello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="73bcb-206">사용 하 여 hello `Remove-AzureApplicationGateway` cmdlet tooremove hello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="73bcb-207">Hello를 사용 하 여 해당 hello 게이트웨이에 제거 되었는지 확인 `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="73bcb-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="73bcb-208">hello 다음 예제에서는 hello `Stop-AzureApplicationGateway` hello 첫 번째 줄에는 cmdlet hello 출력이 차례로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="73bcb-209">중지 된 상태에 hello 응용 프로그램 게이트웨이 사용 하 여 hello `Remove-AzureApplicationGateway` cmdlet tooremove hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="73bcb-210">서비스 hello tooverify 제거 된 hello를 사용할 수 있습니다, `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="73bcb-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="73bcb-211">이 단계는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="73bcb-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73bcb-212">Next steps</span></span>

<span data-ttu-id="73bcb-213">SSL 오프 로드 tooconfigure 참조 [SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="73bcb-214">내부 부하 분산 장치는 응용 프로그램 게이트웨이 toouse tooconfigure 참조 [내부 부하 분산 장치 (ILB) 응용 프로그램 게이트웨이 만들](application-gateway-ilb.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="73bcb-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="73bcb-215">보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:</span><span class="sxs-lookup"><span data-stu-id="73bcb-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="73bcb-216">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="73bcb-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="73bcb-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="73bcb-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
