---
title: "SSL 오프로드 구성 - Azure Application Gateway - PowerShell 클래식 | Microsoft Docs"
description: "이 문서에서는 Azure 클래식 배포 모델을 사용하여 SSL 오프로드와 함께 응용 프로그램 게이트웨이를 만드는 지침을 제공합니다."
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
ms.openlocfilehash: 2eba6fb24c11add12ac16d04d3445e19a3486216
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="dda72-103">클래식 배포 모델을 사용하여 SSL 오프로드에 대한 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="dda72-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dda72-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="dda72-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="dda72-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="dda72-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="dda72-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="dda72-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="dda72-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dda72-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="dda72-108">Azure Application Gateway 구성을 사용하여 웹 팜에서 발생하는 비용이 많이 드는 SSL(Secure Sockets Layer) 암호 해독 작업을 방지하기 위한 게이트웨이에서 SSL 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="dda72-109">SSL 오프로드는 또한 프런트 엔드 서버 설치 및 웹 응용 프로그램의 관리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dda72-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="dda72-110">Before you begin</span></span>

1. <span data-ttu-id="dda72-111">웹 플랫폼 설치 관리자를 사용하는 Azure PowerShell cmdlet의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="dda72-112">**다운로드 페이지** 의 [Windows PowerShell](https://azure.microsoft.com/downloads/)섹션에서 최신 버전을 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="dda72-113">유효한 서브넷과 작업 가상 네트워크가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="dda72-114">서브넷을 사용 중인 가상 컴퓨터 또는 클라우드 배포가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="dda72-115">응용 프로그램 게이트웨이는 가상 네트워크 서브넷에서 단독이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-115">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="dda72-116">응용 프로그램 게이트웨이를 사용하도록 구성된 서버가 존재하거나 가상 네트워크나 공용 IP/VIP가 할당된 해당 끝점이 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="dda72-117">응용 프로그램 게이트웨이에서 SSL 오프로드를 구성하려면 다음 단계를 나열된 순서대로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-117">To configure SSL offload on an application gateway, do the following steps in the order listed:</span></span>

1. [<span data-ttu-id="dda72-118">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="dda72-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="dda72-119">SSL 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="dda72-120">게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="dda72-120">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="dda72-121">게이트웨이 구성 설정</span><span class="sxs-lookup"><span data-stu-id="dda72-121">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="dda72-122">게이트웨이 시작</span><span class="sxs-lookup"><span data-stu-id="dda72-122">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="dda72-123">게이트웨이 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-123">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="dda72-124">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="dda72-124">Create an application gateway</span></span>

<span data-ttu-id="dda72-125">게이트웨이를 생성하려면 `New-AzureApplicationGateway` cmdlet을 사용하여 해당 값을 원하는 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-125">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="dda72-126">게이트웨이에 대한 청구는 이 시점에서 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-126">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="dda72-127">게이트웨이가 성공적으로 작동되면, 요금청구가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-127">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="dda72-128">생성된 게이트웨이의 유효성을 검사하려면 `Get-AzureApplicationGateway` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-128">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="dda72-129">이 샘플에서 *Description*, *InstanceCount* 및 *GatewaySize*는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-129">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="dda72-130">*InstanceCount* 의 기본값은 2이고, 최대값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-130">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="dda72-131">*GatewaySize* 에 대한 기본값은 보통입니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-131">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="dda72-132">크고 작은 다른 사용 가능한 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-132">Small and Large are other available values.</span></span> <span data-ttu-id="dda72-133">게이트웨이가 아직 시작되지 않았으므로 *VirtualIPs* 및 *DnsName*이 빈 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-133">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="dda72-134">이 값들은 게이트웨이가 실행 상태가 되면 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-134">These values are created once the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="dda72-135">SSL 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-135">Upload SSL certificates</span></span>

<span data-ttu-id="dda72-136">`Add-AzureApplicationGatewaySslCertificate`를 사용하여 응용 프로그램 게이트웨이에 *pfx* 형식의 서버 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-136">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span></span> <span data-ttu-id="dda72-137">인증서 이름은 사용자가 선택해야 하고 응용 프로그램 게이트웨이 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="dda72-138">이 인증서는 응용 프로그램 게이트웨이에 대한 모든 인증서 관리작업에 이름이 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="dda72-139">이 다음 예제에서는 cmdlet을 보여 주고 사용자 고유의 샘플 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-139">This following sample shows the cmdlet, replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="dda72-140">그런 다음 인증서 업로드 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-140">Next, validate the certificate upload.</span></span> <span data-ttu-id="dda72-141">`Get-AzureApplicationGatewayCertificate` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-141">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="dda72-142">이 출력 다음 샘플에서는 첫 줄에 cmdlet을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-142">This sample shows the cmdlet on the first line, followed by the output.</span></span>

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
> <span data-ttu-id="dda72-143">인증서 암호는 4~12자의 문자 또는 숫자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-143">The certificate password has to be between 4 to 12 characters, letters, or numbers.</span></span> <span data-ttu-id="dda72-144">특수 문자는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-144">Special characters are not accepted.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="dda72-145">게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="dda72-145">Configure the gateway</span></span>

<span data-ttu-id="dda72-146">응용 프로그램 게이트웨이는 여러 값으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="dda72-147">값은 연결되어 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-147">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="dda72-148">값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-148">The values are:</span></span>

* <span data-ttu-id="dda72-149">**백 엔드 서버 풀:** 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-149">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="dda72-150">나열된 IP 주소는 가상 네트워크 서브넷에 속하거나 공용 IP/VIP이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-150">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="dda72-151">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="dda72-152">이러한 설정은 풀에 연결 및 풀 내의 모든 서버에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-152">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="dda72-153">**프런트 엔드 포트:** 이 포트는 응용 프로그램 게이트웨이에 열려 있는 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-153">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="dda72-154">트래픽이 이 포트에 도달하면, 백 엔드 서버 중의 하나로 리디렉트됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-154">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="dda72-155">**수신기:** 수신기에는 프런트 엔드 포트, 프로토콜(Http 또는 Https, 이 값은 대/소문자 구분) 및 SSL 인증서 이름(SSL 오프로드를 구성하는 경우)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-155">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="dda72-156">**규칙:** 규칙은 수신기와 백 엔드 서버 풀을 바인딩하고 특정 수신기에 도달했을 때 트래픽이 이동되는 백 엔드 서버 풀을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-156">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="dda72-157">현재는 *기본* 규칙만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-157">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="dda72-158">*기본* 규칙은 라운드 로빈 부하 분산입니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-158">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="dda72-159">**추가 구성 정보**</span><span class="sxs-lookup"><span data-stu-id="dda72-159">**Additional configuration notes**</span></span>

<span data-ttu-id="dda72-160">SSL 인증서 구성에서 **HttpListener** 의 프로토콜은 *Https* (대/소문자 구분)로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-160">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="dda72-161">**SslCert** 요소는 이전 SSL 인증서 섹션의 업로드에 사용된 것과 동일한 이름으로 값을 설정하여 **HttpListener**에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-161">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span></span> <span data-ttu-id="dda72-162">프런트 엔드 포트는 443으로 업데이트되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-162">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="dda72-163">**쿠키 기반 선호도를 사용하도록 설정**: 응용 프로그램 게이트웨이는 클라이언트 세션의 요청이 항상 웹 팜에 있는 동일한 VM으로 전송되도록 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-163">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="dda72-164">게이트웨이에서 트래픽을 적절하게 지시할 수 있는 세션 쿠키를 삽입하면 이 시나리오가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-164">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="dda72-165">쿠키 기반 선호도를 사용하려면 **BackendHttpSettings** 요소에서 **CookieBasedAffinity**를 *Enabled*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-165">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="dda72-166">구성 개체를 만들거나, 구성 XML 파일을 사용하여 구성을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="dda72-167">구성 XML 파일을 사용하여 구성을 생성하려면 다음 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-167">To construct your configuration by using a configuration XML file, use the following sample:</span></span>

<span data-ttu-id="dda72-168">**구성 XML 샘플**</span><span class="sxs-lookup"><span data-stu-id="dda72-168">**Configuration XML sample**</span></span>

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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="dda72-169">게이트웨이 구성 설정</span><span class="sxs-lookup"><span data-stu-id="dda72-169">Set the gateway configuration</span></span>

<span data-ttu-id="dda72-170">다음으로, 응용 프로그램 게이트웨이를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-170">Next, you set the application gateway.</span></span> <span data-ttu-id="dda72-171">`Set-AzureApplicationGatewayConfig` cmdlet을 구성 개체 또는 구성 XML 파일과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-171">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="dda72-172">게이트웨이 시작</span><span class="sxs-lookup"><span data-stu-id="dda72-172">Start the gateway</span></span>

<span data-ttu-id="dda72-173">게이트웨이가 구성되면, `Start-AzureApplicationGateway` cmdlet을 사용하여 게이트웨이를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-173">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="dda72-174">응용 프로그램 게이트웨이에 대한 청구는 게이트웨이가 성공적으로 작동된 후 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-174">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="dda72-175">`Start-AzureApplicationGateway` cmdlet을 완료하려면 최대 15-20분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-175">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="dda72-176">게이트웨이 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-176">Verify the gateway status</span></span>

<span data-ttu-id="dda72-177">`Get-AzureApplicationGateway` cmdlet을 사용하여 게이트웨이의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-177">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="dda72-178">`Start-AzureApplicationGateway`가 이전 단계에서 성공한 경우 *상태*가 실행 중이어야 하고, *VirtualIPs*와 *DnsName*에 유효한 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-178">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="dda72-179">이 샘플에서는 응용 프로그램 게이트웨이가 시작, 실행 그리고 트래픽을 받을 준비가 된 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dda72-179">This sample shows an application gateway that is up, running, and is ready to take traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dda72-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dda72-180">Next steps</span></span>

<span data-ttu-id="dda72-181">보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:</span><span class="sxs-lookup"><span data-stu-id="dda72-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="dda72-182">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="dda72-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="dda72-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="dda72-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

