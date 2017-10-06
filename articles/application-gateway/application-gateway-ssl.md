---
title: "-Azure 응용 프로그램 게이트웨이-PowerShell 클래식 aaaConfigure SSL 오프 로드를 | Microsoft Docs"
description: "이 문서를 사용 하 여 응용 프로그램 게이트웨이 ssl 오프 로드 toocreate hello Azure 클래식 배포 모델 하는 지침을 제공 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="5f135-103">Hello 클래식 배포 모델을 사용 하 여 SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="5f135-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f135-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5f135-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="5f135-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f135-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="5f135-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f135-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="5f135-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5f135-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="5f135-108">Azure 응용 프로그램 게이트웨이 hello 게이트웨이 tooavoid 비용이 많이 드는 SSL 암호 해독 작업 toohappen hello 웹 팜에서에 구성 된 tooterminate hello (SECURE Sockets Layer) 세션 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="5f135-109">SSL 오프 로드 hello 프런트 엔드 서버 설치 및 hello 웹 응용 프로그램 관리를 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5f135-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5f135-110">Before you begin</span></span>

1. <span data-ttu-id="5f135-111">Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="5f135-112">다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="5f135-113">유효한 서브넷과 작업 가상 네트워크가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="5f135-114">가상 컴퓨터 또는 클라우드 배포 없습니다 hello 서브넷 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="5f135-115">hello 응용 프로그램 게이트웨이 자체 가상 네트워크 서브넷에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="5f135-116">toouse hello 응용 프로그램 게이트웨이 구성 하는 hello 서버에 존재 해야 하거나 또는 hello 가상 네트워크에서 공용 IP/VIP와 만든 끝점을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="5f135-117">SSL tooconfigure 응용 프로그램 게이트웨이 오프 로드, 나열 된 hello 순서에 단계에 따라 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="5f135-118">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="5f135-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="5f135-119">SSL 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="5f135-120">Hello 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="5f135-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="5f135-121">Hello 게이트웨이 구성 설정</span><span class="sxs-lookup"><span data-stu-id="5f135-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="5f135-122">Hello 게이트웨이 시작</span><span class="sxs-lookup"><span data-stu-id="5f135-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="5f135-123">Hello 게이트웨이 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="5f135-124">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="5f135-124">Create an application gateway</span></span>

<span data-ttu-id="5f135-125">toocreate hello 게이트웨이 사용 하 여 hello `New-AzureApplicationGateway` cmdlet, 사용자의 정보로 hello 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="5f135-126">게이트웨이 hello에 대 한 청구가 시점에서 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="5f135-127">청구는 hello 게이트웨이 성공적으로 시작 하는 경우 이후 단계에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="5f135-128">게이트웨이 hello toovalidate 만들어진 hello를 사용할 수 있습니다, `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5f135-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="5f135-129">Hello 샘플에서 *설명*, *InstanceCount*, 및 *GatewaySize* 는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="5f135-130">기본값에 대 한 hello *InstanceCount* 최대 값이 10 인 2입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="5f135-131">에 대 한 기본값을 hello *GatewaySize* 보통입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="5f135-132">크고 작은 다른 사용 가능한 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-132">Small and Large are other available values.</span></span> <span data-ttu-id="5f135-133">*Virtualip* 및 *DnsName* hello 게이트웨이가 아직 시작 되지 않았습니다. 때문에 출력이 빈 값으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="5f135-134">이러한 값은 hello 게이트웨이 hello 실행 상태가 되 면 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="5f135-135">SSL 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-135">Upload SSL certificates</span></span>

<span data-ttu-id="5f135-136">사용 하 여 `Add-AzureApplicationGatewaySslCertificate` 에 tooupload hello 서버 인증서 *pfx* toohello 응용 프로그램 게이트웨이 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="5f135-137">hello 인증서 이름은 사용자가 선택한 이름 이며 hello 응용 프로그램 게이트웨이 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="5f135-138">이 인증서 참조 tooby hello 응용 프로그램 게이트웨이의 인증서 관리 작업에이 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="5f135-139">사용자의 정보로 hello 샘플 hello 값을 교체이 다음 샘플에서는 hello cmdlet을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="5f135-140">다음으로 hello 인증서 업로드 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="5f135-141">사용 하 여 hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5f135-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="5f135-142">이 hello 출력 다음 샘플에서는 hello 첫 번째 줄에 hello cmdlet을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="5f135-143">hello 인증서 암호가 toobe 4 too12 문자, 문자 또는 숫자 사이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="5f135-144">특수 문자는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="5f135-145">Hello 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="5f135-145">Configure hello gateway</span></span>

<span data-ttu-id="5f135-146">응용 프로그램 게이트웨이는 여러 값으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="5f135-147">hello 값이 연결 될 수 함께 tooconstruct hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="5f135-148">hello 값은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-148">hello values are:</span></span>

* <span data-ttu-id="5f135-149">**백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="5f135-150">나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="5f135-151">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="5f135-152">이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="5f135-153">**프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="5f135-154">트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="5f135-155">**수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="5f135-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="5f135-156">**규칙:** hello 규칙 hello 수신기 및 hello 백 엔드 서버 풀 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="5f135-157">현재만 hello *기본* 규칙 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="5f135-158">hello *기본* 규칙은 라운드 로빈 부하 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="5f135-159">**추가 구성 정보**</span><span class="sxs-lookup"><span data-stu-id="5f135-159">**Additional configuration notes**</span></span>

<span data-ttu-id="5f135-160">SSL 인증서 구성에 대 한 프로토콜에서 hello **HttpListener** 도 변경 해야*Https* (대/소문자 구분).</span><span class="sxs-lookup"><span data-stu-id="5f135-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="5f135-161">hello **SslCert** 요소가 너무 추가**HttpListener** 값이 SSL 인증서 섹션 앞의 hello 업로드에서 사용 되는 이름과 같은 이름을 toohello hello로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="5f135-162">hello 프런트 엔드 포트에는 업데이트 된 too443 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="5f135-163">**tooenable 쿠키 기반 선호도**: 응용 프로그램 게이트웨이 클라이언트 세션에서 요청은 항상 방향이 지정 된 toohello 구성된 tooensure 수 hello 웹 팜의 동일한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="5f135-164">이 시나리오는 hello 게이트웨이 toodirect 트래픽을 적절 하 게 허용 하는 세션 쿠키의 삽입으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="5f135-165">tooenable 쿠키 기반 선호도 설정 **CookieBasedAffinity** 너무*Enabled* hello에 **BackendHttpSettings** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="5f135-166">구성 개체를 만들거나, 구성 XML 파일을 사용하여 구성을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="5f135-167">tooconstruct 구성 XML 파일을 사용 하 여 구성을 사용 하 여 샘플 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="5f135-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="5f135-168">**구성 XML 샘플**</span><span class="sxs-lookup"><span data-stu-id="5f135-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="5f135-169">Hello 게이트웨이 구성 설정</span><span class="sxs-lookup"><span data-stu-id="5f135-169">Set hello gateway configuration</span></span>

<span data-ttu-id="5f135-170">다음으로 hello 응용 프로그램 게이트웨이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="5f135-171">Hello를 사용할 수 있습니다 `Set-AzureApplicationGatewayConfig` cmdlet 구성 개체 또는 구성 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="5f135-172">Hello 게이트웨이 시작</span><span class="sxs-lookup"><span data-stu-id="5f135-172">Start hello gateway</span></span>

<span data-ttu-id="5f135-173">Hello를 사용 하 여 hello 게이트웨이 구성한 후 `Start-AzureApplicationGateway` cmdlet toostart hello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="5f135-174">응용 프로그램 게이트웨이 대 한 청구 hello 게이트웨이 성공적으로 시작 된 후 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="5f135-175">hello `Start-AzureApplicationGateway` cmdlet toofinish too15 20 분이 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="5f135-176">Hello 게이트웨이 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-176">Verify hello gateway status</span></span>

<span data-ttu-id="5f135-177">사용 하 여 hello `Get-AzureApplicationGateway` hello 게이트웨이의 cmdlet toocheck hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="5f135-178">경우 `Start-AzureApplicationGateway` hello 이전 단계에서 성공한 *상태* 실행 해야 하 고 *Virtualip* 및 *DnsName* 유효한 항목 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="5f135-179">이 샘플에서는,를 실행 하 고 길이가 준비 tootake 트래픽이 응용 프로그램 게이트웨이 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f135-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="5f135-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f135-180">Next steps</span></span>

<span data-ttu-id="5f135-181">보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:</span><span class="sxs-lookup"><span data-stu-id="5f135-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="5f135-182">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="5f135-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="5f135-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="5f135-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

