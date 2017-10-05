---
title: "사용자 지정 프로브 만들기 - Azure Application Gateway - PowerShell 클래식 | Microsoft Docs"
description: "클래식 배포 모델에서 PowerShell을 사용하여 응용 프로그램 게이트웨이에 대한 사용자 지정 프로브를 만드는 방법에 대해 알아봅니다."
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: bf190741b10c10e885d927ad21a9f2b25107943f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="3dd41-103">PowerShell을 사용하여 Azure 응용 프로그램 게이트웨이(클래식)에 대한 사용자 지정 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="3dd41-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3dd41-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3dd41-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="3dd41-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dd41-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="3dd41-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dd41-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="3dd41-107">이 문서에서는 PowerShell을 사용하여 기존 응용 프로그램 게이트웨이에 사용자 지정 프로브를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="3dd41-108">사용자 지정 프로브는 특정 상태 확인 페이지를 사용하는 응용 프로그램이나 기본 웹 응용 프로그램에서 성공적으로 응답을 제공하지 않는 응용 프로그램에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3dd41-109">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3dd41-110">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="3dd41-111">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="3dd41-112">[Resource Manager 모델을 사용하여 이러한 단계를 수행하는](application-gateway-create-probe-ps.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-112">Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="3dd41-113">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="3dd41-113">Create an application gateway</span></span>

<span data-ttu-id="3dd41-114">응용 프로그램 게이트웨이를 만들려면</span><span class="sxs-lookup"><span data-stu-id="3dd41-114">To create an application gateway:</span></span>

1. <span data-ttu-id="3dd41-115">응용 프로그램 게이트웨이 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="3dd41-116">구성 XML 파일 또는 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="3dd41-117">구성을 새로 만든 응용 프로그램 게이트웨이 리소스에 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="3dd41-118">사용자 지정 프로브를 사용하여 응용 프로그램 게이트웨이 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="3dd41-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="3dd41-119">게이트웨이를 생성하려면 `New-AzureApplicationGateway` cmdlet을 사용하여 해당 값을 원하는 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="3dd41-120">게이트웨이에 대한 청구는 이 시점에서 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="3dd41-121">게이트웨이가 성공적으로 작동되면, 요금청구가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="3dd41-122">다음 예제에서는 "testvnet1"이라는 가상 네트워크 및 "subnet-1"이라는 서브넷을 사용하여 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="3dd41-123">생성된 게이트웨이의 유효성을 검사하려면 `Get-AzureApplicationGateway` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="3dd41-124">*InstanceCount* 의 기본값은 2이고, 최대값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-124">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="3dd41-125">*GatewaySize* 의 기본값은 보통입니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-125">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="3dd41-126">작게, 보통 및 크게를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="3dd41-127">게이트웨이가 아직 시작되지 않았으므로 *VirtualIPs* 및 *DnsName*이 빈 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="3dd41-128">이 값들은 게이트웨이가 실행 상태가 되면 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="3dd41-129">XML을 사용하여 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="3dd41-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="3dd41-130">다음 예제에서는 XML 파일을 사용하여 모든 응용 프로그램 게이트웨이 설정을 구성하고 응용 프로그램 게이트웨이 리소스에 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="3dd41-131">다음 텍스트를 메모장에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-131">Copy the following text to Notepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="3dd41-132">구성 항목에 대한 괄호 사이의 값을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="3dd41-133">확장명이 .xml인 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="3dd41-134">다음 예제에서는 구성 파일을 사용하여 공용 포트 80에서 HTTP 트래픽의 부하를 분산하는 응용 프로그램 게이트웨이를 설정하고 사용자 지정 프로브를 사용하여 두 IP 주소 사이의 백 엔드 포트 80으로 네트워크 트래픽을 전송하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3dd41-135">Http 또는 Https 프로토콜 항목은 대 소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-135">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="3dd41-136">새 구성 항목 \<Probe\>를 추가하여 사용자 지정 프로브를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="3dd41-137">구성 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="3dd41-137">The configuration parameters are:</span></span>

|<span data-ttu-id="3dd41-138">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-138">Parameter</span></span>|<span data-ttu-id="3dd41-139">설명</span><span class="sxs-lookup"><span data-stu-id="3dd41-139">Description</span></span>|
|---|---|
|<span data-ttu-id="3dd41-140">**Name**</span><span class="sxs-lookup"><span data-stu-id="3dd41-140">**Name**</span></span> |<span data-ttu-id="3dd41-141">사용자 지정 프로브에 대한 참조 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="3dd41-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="3dd41-142">* **Protocol**</span></span> | <span data-ttu-id="3dd41-143">사용되는 프로토콜입니다(가능한 값: HTTP 또는 HTTPS).</span><span class="sxs-lookup"><span data-stu-id="3dd41-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="3dd41-144">**Host** 및 **Path**</span><span class="sxs-lookup"><span data-stu-id="3dd41-144">**Host** and **Path**</span></span> | <span data-ttu-id="3dd41-145">응용 프로그램 게이트웨이에서 인스턴스 상태를 확인하기 위해 호출하는 완전한 URL 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="3dd41-146">예: 웹 사이트가 http://contoso.com/인 경우 프로브를 확인하여 성공적으로 HTTP에 응답하도록 "http://contoso.com/path/custompath.htm"에 대해 사용자 지정 프로브를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="3dd41-147">**간격**</span><span class="sxs-lookup"><span data-stu-id="3dd41-147">**Interval**</span></span> | <span data-ttu-id="3dd41-148">프로브 간격 확인을 구성합니다(단위: 초).</span><span class="sxs-lookup"><span data-stu-id="3dd41-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="3dd41-149">**시간 제한**</span><span class="sxs-lookup"><span data-stu-id="3dd41-149">**Timeout**</span></span> | <span data-ttu-id="3dd41-150">HTTP 응답 확인에 대한 프로브 시간 제한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="3dd41-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="3dd41-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="3dd41-152">백 엔드 인스턴스를 *unhealthy*(비정상) 플래그로 지정하는 데 필요한 실패한 HTTP 응답 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="3dd41-153">프로브 이름은 사용자 지정 프로브 설정에 사용할 백 엔드 풀을 할당하는 \<BackendHttpSettings\> 구성에서 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="3dd41-154">기존 응용 프로그램 게이트웨이에 사용자 지정 프로브 추가</span><span class="sxs-lookup"><span data-stu-id="3dd41-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="3dd41-155">현재 응용 프로그램 게이트웨이 구성 변경에 필요한 세 단계는 현재 XML 구성 파일 가져오기, 사용자 지정 프로브 수정 및 새 XML 설정으로 응용 프로그램 게이트웨이 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="3dd41-156">`Get-AzureApplicationGatewayConfig`을 사용하여 XML 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="3dd41-157">이 cmdlet은 프로브 설정을 추가하기 위해 수정할 XML 구성을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="3dd41-158">텍스트 편집기에서 XML 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="3dd41-159">`<frontendport>` 뒤에 `<probe>` 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="3dd41-160">XML의 backendHttpSettings 섹션에서 다음 예제에 표시된 대로 프로브 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="3dd41-161">XML 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-161">Save the XML file.</span></span>

1. <span data-ttu-id="3dd41-162">`Set-AzureApplicationGatewayConfig`을 사용하여 새 XML 파일로 Application Gateway 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="3dd41-163">이 cmdlet은 Application Gateway를 새 구성으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3dd41-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="3dd41-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3dd41-164">Next steps</span></span>

<span data-ttu-id="3dd41-165">SSL(Secure Sockets Layer) 오프로드를 구성하려는 경우 [SSL 오프로드에 대해 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3dd41-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="3dd41-166">내부 부하 분산 장치에서 사용되도록 응용 프로그램 게이트웨이를 구성하려면 [ILB(내부 부하 분산 장치)를 사용하여 응용 프로그램 게이트웨이 만들기](application-gateway-ilb.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3dd41-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

