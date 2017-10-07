---
title: "사용자 지정 프로브-Azure 응용 프로그램 게이트웨이-PowerShell 클래식 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate 사용자 지정 프로브 응용 프로그램 게이트웨이에 대 한 hello 클래식 배포 모델에서 PowerShell을 사용 하 여 알아봅니다"
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
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="18d83-103">PowerShell을 사용하여 Azure 응용 프로그램 게이트웨이(클래식)에 대한 사용자 지정 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="18d83-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="18d83-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="18d83-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="18d83-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="18d83-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="18d83-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="18d83-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="18d83-107">이 문서에서는 PowerShell과 함께 사용자 지정 프로브 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="18d83-108">사용자 지정 프로브는 특정 상태 확인 페이지를 사용 하는 응용 프로그램 또는 hello 기본 웹 응용 프로그램에 대 한 성공적인 응답을 제공 하지 않는 응용 프로그램에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18d83-109">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="18d83-110">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="18d83-111">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="18d83-112">너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](application-gateway-create-probe-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="18d83-113">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="18d83-113">Create an application gateway</span></span>

<span data-ttu-id="18d83-114">응용 프로그램 게이트웨이 toocreate:</span><span class="sxs-lookup"><span data-stu-id="18d83-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="18d83-115">응용 프로그램 게이트웨이 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="18d83-116">구성 XML 파일 또는 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="18d83-117">새로 만든 응용 프로그램 게이트웨이 리소스 hello 구성 toohello를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="18d83-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="18d83-118">사용자 지정 프로브를 사용하여 응용 프로그램 게이트웨이 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="18d83-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="18d83-119">toocreate hello 게이트웨이 사용 하 여 hello `New-AzureApplicationGateway` cmdlet, 사용자의 정보로 hello 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="18d83-120">게이트웨이 hello에 대 한 청구가 시점에서 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="18d83-121">청구는 hello 게이트웨이 성공적으로 시작 하는 경우 이후 단계에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="18d83-122">hello 다음 예제에서는 응용 프로그램 게이트웨이 "testvnet1"과 "서브넷-1" 이라는 서브넷 이라는 가상 네트워크를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="18d83-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="18d83-123">게이트웨이 hello toovalidate 만들어진 hello를 사용할 수 있습니다, `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18d83-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="18d83-124">기본값에 대 한 hello *InstanceCount* 최대 값이 10 인 2입니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="18d83-125">에 대 한 기본값을 hello *GatewaySize* 보통입니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="18d83-126">작게, 보통 및 크게를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="18d83-127">*Virtualip* 및 *DnsName* hello 게이트웨이가 아직 시작 되지 않았습니다. 때문에 출력이 빈 값으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="18d83-128">이러한 값은 hello 게이트웨이 hello 실행 상태가 되 면 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="18d83-129">XML을 사용하여 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="18d83-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="18d83-130">다음 예제는 hello, 모든 응용 프로그램 게이트웨이 설정 XML 파일 tooconfigure를 사용 하 고 응용 프로그램 게이트웨이 리소스 toohello 커밋하기 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="18d83-131">다음 텍스트 tooNotepad hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-131">Copy hello following text tooNotepad.</span></span>

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

<span data-ttu-id="18d83-132">Hello hello 구성 항목에 대 한 hello 괄호 사이 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="18d83-133">Hello 파일 확장명이.xml으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="18d83-134">hello 다음 예제에서는 응용 프로그램 게이트웨이 tooload hello 구성 파일 tooset toouse 공용 포트 80에서 HTTP 트래픽 균등화 방법과 tooback 끝 포트 80에서 사용자 지정 프로브를 사용 하 여 두 개의 IP 주소 간의 네트워크 트래픽 보내기</span><span class="sxs-lookup"><span data-stu-id="18d83-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18d83-135">Http 또는 Https hello 프로토콜 항목은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="18d83-136">새 구성 항목 \<프로브\> tooconfigure 사용자 지정 프로브 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="18d83-137">hello 구성 매개 변수는.</span><span class="sxs-lookup"><span data-stu-id="18d83-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="18d83-138">매개 변수</span><span class="sxs-lookup"><span data-stu-id="18d83-138">Parameter</span></span>|<span data-ttu-id="18d83-139">설명</span><span class="sxs-lookup"><span data-stu-id="18d83-139">Description</span></span>|
|---|---|
|<span data-ttu-id="18d83-140">**Name**</span><span class="sxs-lookup"><span data-stu-id="18d83-140">**Name**</span></span> |<span data-ttu-id="18d83-141">사용자 지정 프로브에 대한 참조 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="18d83-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="18d83-142">* **Protocol**</span></span> | <span data-ttu-id="18d83-143">사용되는 프로토콜입니다(가능한 값: HTTP 또는 HTTPS).</span><span class="sxs-lookup"><span data-stu-id="18d83-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="18d83-144">**Host** 및 **Path**</span><span class="sxs-lookup"><span data-stu-id="18d83-144">**Host** and **Path**</span></span> | <span data-ttu-id="18d83-145">Hello 인스턴스의 hello 응용 프로그램 게이트웨이 toodetermine hello 상태에서 호출 되는 전체 URL 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="18d83-146">예를 들어 있으면 웹 사이트 http://contoso.com/에 대 한 hello 사용자 지정 프로브를 구성할 수 있습니다 "http://contoso.com/path/custompath.htm" 검색 toohave 성공적인 HTTP 응답을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="18d83-147">**간격**</span><span class="sxs-lookup"><span data-stu-id="18d83-147">**Interval**</span></span> | <span data-ttu-id="18d83-148">Hello 프로브 간격 확인 시간 (초)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="18d83-149">**시간 제한**</span><span class="sxs-lookup"><span data-stu-id="18d83-149">**Timeout**</span></span> | <span data-ttu-id="18d83-150">HTTP 응답 확인에 대 한 hello 프로브 제한 시간을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="18d83-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="18d83-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="18d83-152">필요한 tooflag hello 백 엔드 인스턴스로 실패 한 HTTP 응답 수 hello *비정상*합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="18d83-153">hello 프로브 이름은 hello에서 참조 되 \<BackendHttpSettings\> 구성 tooassign 백 엔드 풀을 사용자 지정 프로브 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="18d83-154">사용자 지정 프로브 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="18d83-155">응용 프로그램 게이트웨이 변경 hello 현재 구성과 3 단계로: hello 현재 XML 구성 파일을 가져오고, toohave 사용자 지정 프로브를 수정 하 고 hello 새 XML 설정을 사용 하 여 hello 응용 프로그램 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="18d83-156">사용 하 여 hello XML 파일을 가져올 `Get-AzureApplicationGatewayConfig`합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="18d83-157">이 cmdlet의 내보내기 hello 구성 XML toobe 프로브 설정이 tooadd를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="18d83-158">텍스트 편집기에서 hello XML 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="18d83-159">`<frontendport>` 뒤에 `<probe>` 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="18d83-160">Hello XML의 hello backendHttpSettings 섹션에서는 hello 다음 예제와 같이 hello 프로브 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

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

  <span data-ttu-id="18d83-161">Hello XML 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-161">Save hello XML file.</span></span>

1. <span data-ttu-id="18d83-162">Hello 사용 하 여 새 XML 파일을 사용한 hello 응용 프로그램 게이트웨이 구성 업데이트 `Set-AzureApplicationGatewayConfig`합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="18d83-163">이 cmdlet는 hello 새 구성을 사용 하 여 응용 프로그램 게이트웨이 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="18d83-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18d83-164">Next steps</span></span>

<span data-ttu-id="18d83-165">Secure Sockets Layer (SSL)를 오프 로드 tooconfigure 참조 [SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="18d83-166">내부 부하 분산 장치는 응용 프로그램 게이트웨이 toouse tooconfigure 참조 [내부 부하 분산 장치 (ILB) 응용 프로그램 게이트웨이 만들](application-gateway-ilb.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18d83-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

