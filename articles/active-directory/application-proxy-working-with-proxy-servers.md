---
title: "aaaWork 기존 온-프레미스 프록시 서버와 Azure AD | Microsoft Docs"
description: "어떻게 toowork을 기존 온-프레미스 프록시 서버에 설명 합니다."
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
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="caedb-103">기존 온-프레미스 프록시 서버 작업</span><span class="sxs-lookup"><span data-stu-id="caedb-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="caedb-104">이 문서에서는 설명 어떻게 아웃 바운드 프록시 서버와 Azure Active Directory (Azure AD) 응용 프로그램 프록시 커넥터 toowork tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="caedb-105">네트워크 환경에 기존 프록시가 있는 고객을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="caedb-106">이러한 주요 배포 시나리오를 살펴보는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="caedb-107">커넥터 toobypass 온-프레미스 아웃 바운드 프록시를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="caedb-108">커넥터 toouse 아웃 바운드 프록시 tooaccess Azure AD 응용 프로그램 프록시를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="caedb-109">커넥터 작동 방법에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="caedb-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="caedb-110">Hello 아웃 바운드 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="caedb-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="caedb-111">아웃 바운드 프록시 사용자 환경에 있으면 적절 한 사용 권한 tooconfigure hello에 대 한 아웃 바운드 프록시 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="caedb-112">Hello 설치 관리자에서 실행 되므로 hello hello 설치를 수행 하는 hello 사용자의 상황에 맞는, Microsoft Edge 또는 다른 인터넷 브라우저를 사용 하 여 hello 구성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="caedb-113">Microsoft Edge의 tooconfigure hello 프록시 설정:</span><span class="sxs-lookup"><span data-stu-id="caedb-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="caedb-114">너무 이동**설정** > **고급 설정 보기** > **프록시 설정 열기** > **수동 프록시 설치** .</span><span class="sxs-lookup"><span data-stu-id="caedb-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="caedb-115">설정 **프록시 서버를 사용 하 여** 너무**에**선택, hello **(인트라넷) 로컬 주소에 프록시 서버 hello를 사용 하지 않는** 확인란을 선택한 다음 변경 hello 주소와 포트 tooreflect 로컬 프록시 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="caedb-116">Hello 필요한 프록시 설정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-116">Fill in hello necessary proxy settings.</span></span>

   ![프록시 설정에 대한 대화 상자](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="caedb-118">아웃바운드 프록시 바이패스</span><span class="sxs-lookup"><span data-stu-id="caedb-118">Bypass outbound proxies</span></span>

<span data-ttu-id="caedb-119">커넥터에는 아웃바운드 요청을 하는 기본 OS 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="caedb-120">이러한 구성 요소는 자동 toolocate hello 네트워크에서 프록시 서버를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="caedb-121">Hello 환경에서 사용 하는 경우 웹 프록시 자동 검색 (WPAD) 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="caedb-122">hello OS 구성 요소는 wpad.domainsuffix에 대 한 DNS 조회를 수행 하 여 toolocate 프록시 서버를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="caedb-123">이 DNS에 확인 되 면 HTTP은 다음 요청이 toohello IP wpad.dat에 대 한 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="caedb-124">이 요청에는 사용자 환경에서 프록시 구성 스크립트 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="caedb-125">hello 커넥터가 스크립트 tooselect 아웃 바운드 프록시 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="caedb-126">그러나 커넥터 트래픽은 수 여전히 통과 하지, hello 프록시에 필요한 추가 구성 설정으로 인해 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="caedb-127">사용 하 여 온-프레미스 프록시 tooensure 직접 연결 toohello Azure hello 커넥터 toobypass를 구성할 수 있습니다 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="caedb-128">(네트워크 정책에 대 한 허용) 하는 경우이 접근 방법이 권장 적은 하나의 구성 toomaintain 있다고 의미 하기 때문에, 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="caedb-129">hello C:\Program Files\Microsoft AAD 응용 프로그램 프록시 Connector\ApplicationProxyConnectorService.exe.config 파일을 편집 하 고 hello를 추가 하는 hello 커넥터에 대 한 아웃 바운드 프록시 사용 toodisable *system.net* 이 코드 예제에 표시 된 섹션 :</span><span class="sxs-lookup"><span data-stu-id="caedb-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

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
<span data-ttu-id="caedb-130">tooensure hello 커넥터 업데이트 프로그램 서비스 hello 프록시를 바이패스 하는 C:\Program Files\Microsoft AAD 응용 프로그램 프록시 커넥터 업데이트 프로그램에 있는 유사한 변경 toohello ApplicationProxyConnectorUpdaterService.exe.config 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="caedb-131">Hello 원본 파일의 있는지 toomake 복사본 수 있게 toorevert toohello 기본.config 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="caedb-132">Hello 아웃 바운드 프록시 서버 사용</span><span class="sxs-lookup"><span data-stu-id="caedb-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="caedb-133">일부 환경 예외 없이 아웃 바운드 프록시를 통해 모든 아웃 바운드 트래픽을 toogo가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="caedb-134">결과적으로, hello 프록시 바이패스 하 고 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="caedb-135">Hello 다음 다이어그램에에서 나와 있는 것 처럼 hello 커넥터 트래픽 toogo hello 아웃 바운드 프록시를 통해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![아웃 바운드 프록시 tooAzure AD 통해 트래픽을 toogo 커넥터 구성 응용 프로그램 프록시](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="caedb-137">따라서 아웃 바운드 트래픽을 having,이 없는 필요 tooconfigure 인바운드 방화벽을 통해 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="caedb-138">1 단계: hello 커넥터를 구성 및 관련 서비스 toogo hello 아웃 바운드 프록시를 통해</span><span class="sxs-lookup"><span data-stu-id="caedb-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="caedb-139">Hello 커넥터 hello 아웃 바운드 프록시 서버 및 시도 toouse이 자동으로 검색 WPAD hello 환경에서 사용 되 고 적절 하 게 구성 하는 경우 앞에서 설명, 것입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="caedb-140">그러나 hello 커넥터 toogo 아웃 바운드 프록시를 통해 명시적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="caedb-141">따라서 hello C:\Program Files\Microsoft AAD 응용 프로그램 프록시 Connector\ApplicationProxyConnectorService.exe.config 파일을 편집 및 hello 추가 toodo *system.net* 이 코드 예제에 표시 된 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="caedb-142">변경 *proxyserver:8080* tooreflect 로컬 프록시 서버 이름 또는 IP 주소 및 hello 포트에서 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

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

<span data-ttu-id="caedb-143">다음으로 C:\Program Files\Microsoft AAD 응용 프로그램 프록시 커넥터 Updater\ApplicationProxyConnectorUpdaterService.exe.config 있는 비슷한 변경 toohello 파일 하 여 hello 커넥터 업데이트 프로그램 서비스 toouse hello 프록시를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="caedb-144">2 단계: 구성 hello 커넥터를 통해 관련된 서비스 tooflow hello 프록시 tooallow 트래픽</span><span class="sxs-lookup"><span data-stu-id="caedb-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="caedb-145">4 개의 측면 tooconsider hello 아웃 바운드 프록시에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="caedb-146">프록시 아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="caedb-146">Proxy outbound rules</span></span>
* <span data-ttu-id="caedb-147">프록시 인증</span><span class="sxs-lookup"><span data-stu-id="caedb-147">Proxy authentication</span></span>
* <span data-ttu-id="caedb-148">프록시 포트</span><span class="sxs-lookup"><span data-stu-id="caedb-148">Proxy ports</span></span>
* <span data-ttu-id="caedb-149">SSL 조사</span><span class="sxs-lookup"><span data-stu-id="caedb-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="caedb-150">프록시 아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="caedb-150">Proxy outbound rules</span></span>
<span data-ttu-id="caedb-151">커넥터 서비스 액세스에 대 한 끝점을 다음 액세스 toohello 허용:</span><span class="sxs-lookup"><span data-stu-id="caedb-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="caedb-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="caedb-152">*.msappproxy.net</span></span>
* <span data-ttu-id="caedb-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="caedb-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="caedb-154">초기 등록에 대 한 끝점을 다음 액세스 toohello 허용:</span><span class="sxs-lookup"><span data-stu-id="caedb-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="caedb-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="caedb-155">login.windows.net</span></span>
* <span data-ttu-id="caedb-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="caedb-156">login.microsoftonline.com</span></span>

<span data-ttu-id="caedb-157">FQDN으로 연결 허용 대신 toospecify IP 범위를 할 수 없는 경우이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="caedb-158">Tooall 대상 hello 커넥터에 대 한 아웃 바운드 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="caedb-159">너무 hello 커넥터에 대 한 아웃 바운드 액세스를 허용[Azure 데이터 센터 IP 범위](https://www.microsoft.com/en-gb/download/details.aspx?id=41653)합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="caedb-160">Azure 데이터 센터 IP 범위 목록이 hello를 사용 하 여 hello 챌린지는 매주 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="caedb-161">해야 tooput 내의 프로세스에 위치 tooensure 액세스 규칙에 따라 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="caedb-162">프록시 인증</span><span class="sxs-lookup"><span data-stu-id="caedb-162">Proxy authentication</span></span>

<span data-ttu-id="caedb-163">프록시 인증은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="caedb-164">현재 권장 하는 것은 tooallow hello 커넥터 익명 액세스 toohello 인터넷 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="caedb-165">프록시 포트</span><span class="sxs-lookup"><span data-stu-id="caedb-165">Proxy ports</span></span>

<span data-ttu-id="caedb-166">hello 커넥터 hello CONNECT 메서드를 사용 하 여 SSL 기반 아웃 바운드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="caedb-167">기본적으로이 메서드는 hello 아웃 바운드 프록시를 통해 터널을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="caedb-168">Hello 프록시 서버 tooallow 443 및 80 tooports 터널링을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="caedb-169">Service Bus가 HTTPS를 초과하면 포트 443을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="caedb-170">그러나 기본적으로 서비스 버스 직접 TCP 연결을 시도 되 고 다시 tooHTTPS 직접 연결에 실패 하는 경우에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="caedb-171">tooensure hello 아웃 바운드 프록시 서버를 통해 트래픽이도 전송 되는 서비스 버스 hello, 해당 hello 커넥터 toohello 직접 연결할 수 없는 확인 하는 포트 9350, 9352, 및 5671 용 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="caedb-172">SSL 조사</span><span class="sxs-lookup"><span data-stu-id="caedb-172">SSL inspection</span></span>
<span data-ttu-id="caedb-173">Hello 커넥터 트래픽에 대 한 문제를 일으키기 때문에 hello 커넥터 트래픽에 대 한 SSL 검사를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="caedb-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="caedb-174">커넥터 프록시 및 서비스 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="caedb-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="caedb-175">이제 hello 프록시를 통과 하는 모든 트래픽이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="caedb-176">문제가 있는 경우 다음 문제 해결 정보는 hello 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="caedb-177">가장 좋은 방법은 tooidentify hello 및 커넥터 연결 문제 해결을 hello 커넥터 서비스를 시작 하는 동안 hello 커넥터 서비스에서 네트워크 캡처 tootake 문제의 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="caedb-178">이는 어려운 작업일 수 있으므로 네트워크 추적을 캡처 및 필터링하는 빠른 팁을 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="caedb-179">선택한 도구를 모니터링 하는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="caedb-180">Hello이이 문서에서는 Microsoft Network Monitor 3.4 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="caedb-181">[Microsoft에서 다운로드](https://www.microsoft.com/download/details.aspx?id=4865)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="caedb-182">hello 예제 및 hello 다음 섹션에서에서 사용 하는 필터는 특정 tooNetwork 모니터, 하지만 hello 원칙 적용된 tooany 분석 도구가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="caedb-183">네트워크 모니터를 사용하여 캡처</span><span class="sxs-lookup"><span data-stu-id="caedb-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="caedb-184">toostart 캡처:</span><span class="sxs-lookup"><span data-stu-id="caedb-184">toostart a capture:</span></span>

1. <span data-ttu-id="caedb-185">네트워크 모니터를 열고 **새 캡처**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="caedb-186">Hello 클릭 **시작** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-186">Click hello **Start** button.</span></span>

   ![네트워크 모니터 창](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="caedb-188">캡처를 완료 한 후 클릭 hello **중지** 단추 tooend 것입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="caedb-189">커넥터 트래픽 캡처</span><span class="sxs-lookup"><span data-stu-id="caedb-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="caedb-190">초기 문제 해결을 위해 수행할 단계를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="caedb-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="caedb-191">Services.msc를에서 hello Azure AD 응용 프로그램 프록시 커넥터 서비스를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="caedb-192">Hello 네트워크 캡처를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-192">Start hello network capture.</span></span>
3. <span data-ttu-id="caedb-193">Hello Azure AD 응용 프로그램 프록시 커넥터 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="caedb-194">Hello 네트워크 캡처를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-194">Stop hello network capture.</span></span>

   ![services.msc의 Azure AD 응용 프로그램 프록시 커넥터 서비스](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="caedb-196">Hello 커넥터 toohello 프록시 서버에서 hello 요청 확인</span><span class="sxs-lookup"><span data-stu-id="caedb-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="caedb-197">이제 네트워크 캡처를가지고 하 준비 toofilter 것입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="caedb-198">hello 추적 hello 키 toolooking toofilter hello 캡처 방법을 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="caedb-199">필터가 두 개는 다음과 같습니다 (여기서: hello 모드 해제 프록시 서비스 포트는 8080)입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="caedb-200">**(http.Request 또는 http.Response) 및 tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="caedb-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="caedb-201">Hello에이 필터를 입력 하면 **표시 필터** 창과 선택 **적용**, 캡처된 hello 트래픽 hello 필터에 따라 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="caedb-202">hello 이전 필터 표시 hello HTTP 요청 및 응답 방금 hello 모드 해제 프록시 포트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="caedb-203">여기서 hello 커넥터는 구성 된 프록시 서버 toouse 커넥터 시작을 위한 hello 필터 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![필터링된 HTTP 요청 및 응답의 예제 목록](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="caedb-205">이제 구체적으로 원하는 hello hello 프록시 서버와의 통신을 보여 주는 연결 요청에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="caedb-206">성공하면 HTTP OK(200) 응답을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="caedb-207">407 또는 502, 같은 다른 응답 코드에 표시 되 면 hello 프록시 인증을 요구 되었거나 다른 이유로 hello 트래픽을 허용 하지 않도록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="caedb-208">이 시점에는 프록시 서버 지원 팀이 관여합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="caedb-209">실패한 TCP 연결 시도 식별</span><span class="sxs-lookup"><span data-stu-id="caedb-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="caedb-210">hello에 관심이 있을 수 있습니다 하는 다른 일반적인 시나리오는 hello 커넥터 시도 tooconnect를 직접 하지만 실패 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="caedb-211">다음은 tooeasily이이 문제를 식별에 도움이 되는 다른 네트워크 모니터 필터가입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="caedb-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="caedb-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="caedb-213">SYN 패킷을 hello 첫 번째 패킷이 전송 tooestablish TCP 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="caedb-214">이 패킷 응답은 반환 하지 않습니다, hello SYN 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="caedb-215">모든 재전송 된 SYNs hello 필터 toosee 앞에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="caedb-216">그런 다음 이러한 SYNs tooany 커넥터 관련 트래픽와 일치 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="caedb-217">hello 다음 예제는 실패 한 연결을 시도 하는 9352 tooService 버스 포트.</span><span class="sxs-lookup"><span data-stu-id="caedb-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![실패한 연결 시도의 예제 응답](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="caedb-219">앞에 응답 하는 hello 같은 결과 볼 경우 hello 커넥터 hello Azure 서비스 버스 서비스를 사용 하 여 직접 toocommunicate를 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="caedb-220">Hello 커넥터 toomake 직접 연결 toohello Azure 예상 되는 경우 서비스를이 응답은 뚜렷한 네트워크 또는 방화벽 문제가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="caedb-221">프록시 서버 구성된 toouse 인 경우이 응답 서비스 버스가 HTTPS를 통해 연결 tooattempting 전환 하기 전에 직접 TCP 연결을 시도 하 의미할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="caedb-222">네트워크 추적 분석은 만능 도구는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="caedb-223">하지만 네트워크의 진행 상황에 대 한 중요 한 도구 tooget 요약 정보를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="caedb-224">커넥터 연결 문제가 있는 toostruggle를 계속 진행 하면 지원 팀으로 티켓을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="caedb-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="caedb-225">hello 팀 추가 문제 해결을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caedb-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="caedb-226">응용 프로그램 프록시 커넥터와 관련된 오류를 해결하는 방법에 대한 자세한 내용은 [응용 프로그램 프록시 문제 해결](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="caedb-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="caedb-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="caedb-227">Next steps</span></span>

[<span data-ttu-id="caedb-228">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="caedb-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="caedb-229">
[Toosilently hello Azure AD 응용 프로그램 프록시 커넥터를 설치 하는 방법](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="caedb-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
