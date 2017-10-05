---
title: "기존 온-프레미스 프록시 서버 및 Azure AD 작업 | Microsoft Docs"
description: "기존 온-프레미스 프록시 서버로 작업하는 방법을 다룹니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="429f1-103">기존 온-프레미스 프록시 서버 작업</span><span class="sxs-lookup"><span data-stu-id="429f1-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="429f1-104">이 문서에서는 아웃바운드 프록시 서버로 작업하도록 Azure AD(Azure Active Directory) 응용 프로그램 프록시 커넥터를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="429f1-105">네트워크 환경에 기존 프록시가 있는 고객을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="429f1-106">이러한 주요 배포 시나리오를 살펴보는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="429f1-107">온-프레미스 아웃바운드 프록시를 바이패스하도록 커넥터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="429f1-108">아웃바운드 프록시를 사용하여 Azure AD 응용 프로그램 프록시에 액세스하도록 커넥터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="429f1-109">커넥터 작동 방법에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="429f1-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="429f1-110">아웃바운드 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="429f1-110">Configure the outbound proxy</span></span>

<span data-ttu-id="429f1-111">해당 환경에 아웃바운드 프록시가 있는 경우 적절한 사용 권한이 있는 계정을 사용하여 아웃바운드 프록시를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-111">If you have an outbound proxy in your environment, use an account with appropriate permissions to configure the outbound proxy.</span></span> <span data-ttu-id="429f1-112">설치 관리자가 설치를 수행하는 사용자의 컨텍스트에서 실행되기 때문에 Microsoft Edge 또는 다른 인터넷 브라우저를 사용하여 구성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-112">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="429f1-113">Microsoft Edge에서 프록시 설정을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="429f1-113">To configure the proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="429f1-114">**설정** > **고급 설정 보기** > **프록시 설정 열기** > **수동 프록시 설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-114">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="429f1-115">**프록시 서버 사용**을 **켜기**로 설정하고 **로컬 (인트라넷) 주소에 프록시 서버 사용 안 함** 확인란을 선택한 후 주소 및 포트를 변경하여 로컬 프록시 서버를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-115">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="429f1-116">필요한 프록시 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-116">Fill in the necessary proxy settings.</span></span>

   ![프록시 설정에 대한 대화 상자](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="429f1-118">아웃바운드 프록시 바이패스</span><span class="sxs-lookup"><span data-stu-id="429f1-118">Bypass outbound proxies</span></span>

<span data-ttu-id="429f1-119">커넥터에는 아웃바운드 요청을 하는 기본 OS 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="429f1-120">이러한 구성 요소는 자동으로 네트워크에서 프록시 서버를 찾으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-120">These components automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="429f1-121">환경에서 사용하도록 설정된 경우 WPAD(웹 프록시 자동 검색)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="429f1-122">OS 구성 요소는 wpad.domainsuffix에 대한 DNS 조회를 수행하여 프록시 서버를 찾아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-122">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="429f1-123">DNS에서 확인되면 wpad.dat에 대한 IP 주소에 HTTP를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-123">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="429f1-124">이 요청은 사용자 환경에서 프록시 구성 스크립트가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-124">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="429f1-125">커넥터는 이 스크립트를 사용하여 아웃바운드 프록시 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-125">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="429f1-126">하지만 커넥터 트래픽은 프록시에서 필요한 추가 구성 설정 때문에 여전히 통과하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-126">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="429f1-127">온-프레미스 프록시를 바이패스하여 Azure 서비스로 직접 연결을 사용하도록 커넥터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-127">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="429f1-128">이렇게 하면 유지할 구성이 줄어들기 때문에 네트워크 정책에서 허용하기만 한다면 이 방법을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="429f1-129">커넥터에 아웃바운드 프록시 사용을 사용하지 않도록 설정하려면 C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config 파일을 편집하여 다음 코드 샘플에 표시된 *system.net* 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-129">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="429f1-130">커넥터 업데이터 서비스도 프록시를 바이패스하도록 하려면 C:\Program Files\Microsoft AAD App Proxy Connector Updater에 위치한 ApplicationProxyConnectorUpdaterService.exe.config 파일을 유사하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-130">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="429f1-131">기본 .config 파일로 되돌려야 할 경우를 대비해 원본 파일을 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-131">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="429f1-132">아웃바운드 프록시 서버 사용</span><span class="sxs-lookup"><span data-stu-id="429f1-132">Use the outbound proxy server</span></span>

<span data-ttu-id="429f1-133">일부 환경에서는 모든 아웃바운드 트래픽이 예외 없이 아웃바운드 프록시를 통과해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-133">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="429f1-134">따라서 프록시를 바이패스하는 것은 옵션이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-134">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="429f1-135">다음 다이어그램에 표시된 대로 커넥터 트래픽이 아웃바운드 프록시를 통과하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-135">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![Azure AD 응용 프로그램 프록시에 대한 아웃바운드 프록시를 통과하도록 커넥터 트래픽 구성](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="429f1-137">그 결과 아웃바운드 트래픽만 포함되므로 방화벽을 통과하는 인바운드 액세스를 구성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-137">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="429f1-138">1단계: 아웃바운드 프록시를 통과하도록 커넥터 및 관련 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="429f1-138">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="429f1-139">앞서 설명한 것처럼 환경에 WPAD가 사용되고 적절히 구성된 경우 커넥터는 아웃바운드 프록시 서버를 자동으로 검색하고 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-139">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="429f1-140">하지만 트래픽이 아웃바운드 프록시를 통과하도록 명시적으로 커넥터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-140">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="429f1-141">이렇게 하려면 C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config 파일을 편집하여 다음 코드 샘플에 표시된 *system.net* 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-141">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="429f1-142">로컬 프록시 서버 이름 또는 IP 주소와 수신 대기 중인 포트를 반영하도록 *proxyserver:8080*을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-142">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="429f1-143">그런 다음 C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config에 위치한 파일을 유사하게 변경하여 프록시를 사용하도록 커넥터 업데이터 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-143">Next, configure the Connector Updater service to use the proxy by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="429f1-144">2단계: 커넥터 및 관련 서비스에서 트래픽이 통과하여 흐를 수 있도록 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="429f1-144">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="429f1-145">아웃바운드 프록시에서는 다음 4가지 측면을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-145">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="429f1-146">프록시 아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="429f1-146">Proxy outbound rules</span></span>
* <span data-ttu-id="429f1-147">프록시 인증</span><span class="sxs-lookup"><span data-stu-id="429f1-147">Proxy authentication</span></span>
* <span data-ttu-id="429f1-148">프록시 포트</span><span class="sxs-lookup"><span data-stu-id="429f1-148">Proxy ports</span></span>
* <span data-ttu-id="429f1-149">SSL 조사</span><span class="sxs-lookup"><span data-stu-id="429f1-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="429f1-150">프록시 아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="429f1-150">Proxy outbound rules</span></span>
<span data-ttu-id="429f1-151">커넥터 서비스 액세스를 위해 다음 끝점에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-151">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="429f1-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="429f1-152">*.msappproxy.net</span></span>
* <span data-ttu-id="429f1-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="429f1-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="429f1-154">초기 등록을 위해 다음 끝점에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-154">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="429f1-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="429f1-155">login.windows.net</span></span>
* <span data-ttu-id="429f1-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="429f1-156">login.microsoftonline.com</span></span>

<span data-ttu-id="429f1-157">FQDN으로 연결을 허용할 수 없고 그 대신 IP 범위를 지정해야 하는 경우 다음 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-157">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="429f1-158">모든 대상에 대한 커넥터 아웃바운드 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="429f1-158">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="429f1-159">[Azure 데이터 센터 IP 범위](https://www.microsoft.com/en-gb/download/details.aspx?id=41653)에 대한 커넥터 아웃바운드 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="429f1-159">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="429f1-160">Azure 데이터 센터 IP 범위 목록의 사용과 관련된 문제는 매주 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-160">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="429f1-161">액세스 규칙을 적절하게 업데이트하도록 프로세스를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-161">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="429f1-162">프록시 인증</span><span class="sxs-lookup"><span data-stu-id="429f1-162">Proxy authentication</span></span>

<span data-ttu-id="429f1-163">프록시 인증은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="429f1-164">현재 권장 사항은 인터넷 대상에 대한 커넥터 익명 액세스를 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-164">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="429f1-165">프록시 포트</span><span class="sxs-lookup"><span data-stu-id="429f1-165">Proxy ports</span></span>

<span data-ttu-id="429f1-166">커넥터는 CONNECT 메서드를 사용하여 아웃바운드 SSL 기반 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-166">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="429f1-167">이 메서드는 기본적으로 아웃바운드 프록시를 통해 터널을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-167">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="429f1-168">비표준 SSL 포트 443 및 80으로 터널링을 허용하도록 프록시 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-168">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="429f1-169">Service Bus가 HTTPS를 초과하면 포트 443을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="429f1-170">하지만 기본적으로 Service Bus는 직접 TCP 연결을 시도하며 직접 연결이 실패할 때만 HTTPS를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-170">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="429f1-171">Service Bus 트래픽이 아웃바운드 프록시 서버를 통해 전송되도록 하려면 커넥터에서 포트 9350, 9352 및 5671로 Azure 서비스에 직접 연결할 수 없음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-171">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="429f1-172">SSL 조사</span><span class="sxs-lookup"><span data-stu-id="429f1-172">SSL inspection</span></span>
<span data-ttu-id="429f1-173">커넥터 트래픽에 대한 문제를 발생시키기 때문에 커넥터 트래픽에 대한 SSL 검사를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-173">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="429f1-174">커넥터 프록시 및 서비스 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="429f1-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="429f1-175">이제 프록시를 통과하여 흐르는 모든 트래픽이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-175">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="429f1-176">문제가 있는 경우 다음 문제 해결 정보가 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-176">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="429f1-177">커넥터 연결 문제를 식별하고 해결하는 좋은 방법은 커넥터 서비스를 시작하는 동안 커넥터 서비스에서 네트워크 캡처를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-177">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="429f1-178">이는 어려운 작업일 수 있으므로 네트워크 추적을 캡처 및 필터링하는 빠른 팁을 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="429f1-179">원하는 모니터링 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-179">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="429f1-180">이 문서에서는 Microsoft 네트워크 모니터 3.4를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-180">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="429f1-181">[Microsoft에서 다운로드](https://www.microsoft.com/download/details.aspx?id=4865)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="429f1-182">다음 섹션에서 사용하는 예제와 필터는 네트워크 모니터에 국한되지만 원리는 모든 분석 도구에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-182">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="429f1-183">네트워크 모니터를 사용하여 캡처</span><span class="sxs-lookup"><span data-stu-id="429f1-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="429f1-184">캡처를 시작하려면:</span><span class="sxs-lookup"><span data-stu-id="429f1-184">To start a capture:</span></span>

1. <span data-ttu-id="429f1-185">네트워크 모니터를 열고 **새 캡처**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="429f1-186">**시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-186">Click the **Start** button.</span></span>

   ![네트워크 모니터 창](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="429f1-188">캡처를 완료한 후에 **중지** 단추를 클릭하여 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-188">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="429f1-189">커넥터 트래픽 캡처</span><span class="sxs-lookup"><span data-stu-id="429f1-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="429f1-190">초기 문제 해결의 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-190">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="429f1-191">services.msc에서 Azure AD 응용 프로그램 프록시 커넥터 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-191">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="429f1-192">네트워크 캡처를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-192">Start the network capture.</span></span>
3. <span data-ttu-id="429f1-193">Azure AD 응용 프로그램 프록시 커넥터 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-193">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="429f1-194">네트워크 캡처를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-194">Stop the network capture.</span></span>

   ![services.msc의 Azure AD 응용 프로그램 프록시 커넥터 서비스](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="429f1-196">커넥터에서 프록시 서버에 대한 요청 확인</span><span class="sxs-lookup"><span data-stu-id="429f1-196">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="429f1-197">이제 네트워크 캡처를 가져왔으므로 필터링할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-197">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="429f1-198">추적을 살펴보기 위해서는 캡처를 필터링하는 방법을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-198">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="429f1-199">한 가지 필터는 다음과 같습니다(여기서 8080은 프록시 서비스 포트).</span><span class="sxs-lookup"><span data-stu-id="429f1-199">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="429f1-200">**(http.Request 또는 http.Response) 및 tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="429f1-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="429f1-201">**필터 표시** 창에 이 필터를 입력하고 **적용**을 선택하면 필터를 토대로 캡처한 트래픽을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-201">If you enter this filter in the **Display Filter** window and select **Apply**, it filters the captured traffic based on the filter.</span></span>

<span data-ttu-id="429f1-202">이전 필터는 프록시 포트로 보내거나 받는 HTTP 요청 및 응답만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-202">The preceding filter shows just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="429f1-203">프록시 서버를 사용하도록 구성된 커넥터를 시작하면 필터는 다음과 같은 내용을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-203">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![필터링된 HTTP 요청 및 응답의 예제 목록](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="429f1-205">구체적으로 프록시 서버와 통신을 보여 주는 CONNECT 요청을 찾는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-205">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="429f1-206">성공하면 HTTP OK(200) 응답을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="429f1-207">다른 응답 코드(예: 407 또는 502)가 표시되면 프록시에서 인증을 요청 중이고 다른 이유로 트래픽을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-207">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="429f1-208">이 시점에는 프록시 서버 지원 팀이 관여합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="429f1-209">실패한 TCP 연결 시도 식별</span><span class="sxs-lookup"><span data-stu-id="429f1-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="429f1-210">사용자는 커넥터가 직접 연결을 시도하지만 실패하는 다른 일반적인 시나리오도 파악하고 싶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-210">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="429f1-211">이 문제를 쉽게 식별하는 데 도움이 되는 다른 네트워크 모니터 필터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-211">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="429f1-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="429f1-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="429f1-213">SYN 패킷은 TCP 연결을 설정하기 위해 전송된 첫 번째 패킷입니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-213">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="429f1-214">이 패킷이 응답을 반환하지 않으면 SYN이 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-214">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="429f1-215">이전 필터를 사용하여 재전송된 SYN을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-215">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="429f1-216">그런 다음 이러한 SYN이 커넥터와 관련된 트래픽에 해당하는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-216">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="429f1-217">다음 예제에서는 Service Bus 포트 9352에 대해 실패한 연결 시도를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-217">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![실패한 연결 시도의 예제 응답](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="429f1-219">이전 응답과 같은 항목이 표시되면 커넥터는 Azure Service Bus 서비스와 직접 통신을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-219">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="429f1-220">커넥터를 Azure 서비스에 직접 연결하려는 경우 이 응답으로 인해 네트워크 또는 방화벽 문제가 있음을 확실히 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-220">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="429f1-221">프록시 서버를 사용하도록 구성한 경우 이 응답은 Service Bus에서 HTTPS를 통한 연결로 전환하기 전에 직접 TCP 연결을 시도한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-221">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="429f1-222">네트워크 추적 분석은 만능 도구는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="429f1-223">하지만 네트워크에서 어떤 일이 발생하는지에 대한 정보를 빨리 알아낼 수 있는 유용한 도구일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-223">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="429f1-224">커넥터 연결 문제가 계속 발생하는 경우 지원 팀을 사용하여 티켓을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="429f1-224">If you continue to struggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="429f1-225">팀은 추가 문제 해결을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="429f1-225">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="429f1-226">응용 프로그램 프록시 커넥터와 관련된 오류를 해결하는 방법에 대한 자세한 내용은 [응용 프로그램 프록시 문제 해결](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="429f1-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="429f1-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="429f1-227">Next steps</span></span>

[<span data-ttu-id="429f1-228">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="429f1-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="429f1-229">
[Azure AD 응용 프로그램 프록시 커넥터를 자동으로 설치하는 방법](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="429f1-229">
[How to silently install the Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
