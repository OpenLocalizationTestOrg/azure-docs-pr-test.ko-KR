---
title: "Azure AD 응용 프로그램 프록시에 대한 보안 고려 사항 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시를 사용하는 경우 보안 고려 사항 설명"
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
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: c6ead651133eb17fd55f7567cdb14dc3bcd64245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a><span data-ttu-id="7b2dc-103">Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="7b2dc-103">Security considerations for accessing apps remotely with Azure AD Application Proxy</span></span>

<span data-ttu-id="7b2dc-104">이 문서에서는 Azure Active Directory 응용 프로그램 프록시 서비스에서 응용 프로그램을 원격으로 게시 및 액세스하기 위한 안전한 서비스를 제공하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-104">This article explains how Azure Active Directory Application Proxy provides a secure service for publishing and accessing your applications remotely.</span></span>

<span data-ttu-id="7b2dc-105">다음 다이어그램은 Azure AD를 통해 온-프레미스 응용 프로그램에 안전하게 원격으로 액세스할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-105">The following diagram shows how Azure AD enables secure remote access to your on-premises applications.</span></span>

 ![Azure AD 응용 프로그램 프록시를 통한 보안 원격 액세스의 다이어그램](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a><span data-ttu-id="7b2dc-107">보안 이점</span><span class="sxs-lookup"><span data-stu-id="7b2dc-107">Security benefits</span></span>

<span data-ttu-id="7b2dc-108">Azure AD 응용 프로그램 프록시는 다음과 같은 보안 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-108">Azure AD Application Proxy offers the following security benefits:</span></span>

### <a name="authenticated-access"></a><span data-ttu-id="7b2dc-109">인증된 액세스</span><span class="sxs-lookup"><span data-stu-id="7b2dc-109">Authenticated access</span></span> 

<span data-ttu-id="7b2dc-110">Azure Active Directory 사전 인증을 사용하도록 선택한 경우 인증된 연결만 네트워크에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-110">If you choose to use Azure Active Directory preauthentication, then only authenticated connections can access your network.</span></span>

<span data-ttu-id="7b2dc-111">Azure AD 응용 프로그램 프록시는 모든 인증에 Azure AD STS(보안 토큰 서비스)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-111">Azure AD Application Proxy relies on the Azure AD security token service (STS) for all authentication.</span></span>  <span data-ttu-id="7b2dc-112">사전 인증은 인증된 ID만 백 엔드 응용 프로그램에 액세스할 수 있기 때문에 본질적으로 많은 수의 익명 공격을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-112">Preauthentication, by its very nature, blocks a significant number of anonymous attacks, because only authenticated identities can access the back-end application.</span></span>

<span data-ttu-id="7b2dc-113">사전 인증 방법으로 통과를 선택하면 이러한 이점을 활용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-113">If you choose Passthrough as your preauthentication method, you don't get this benefit.</span></span> 

### <a name="conditional-access"></a><span data-ttu-id="7b2dc-114">조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="7b2dc-114">Conditional access</span></span>

<span data-ttu-id="7b2dc-115">네트워크 연결이 설정되기 전에 다양한 정책 제어를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-115">Apply richer policy controls before connections to your network are established.</span></span>

<span data-ttu-id="7b2dc-116">[조건부 액세스](active-directory-conditional-access-azuread-connected-apps.md)를 사용하면 백 엔드 응용 프로그램에 액세스할 수 있는 트래픽에 대한 제한을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-116">With [conditional access](active-directory-conditional-access-azuread-connected-apps.md), you can define restrictions on what traffic is allowed to access your back-end applications.</span></span> <span data-ttu-id="7b2dc-117">위치, 인증 강도 및 사용자 위험 프로필에 따라 로그인을 제한하는 정책을 사항을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-117">You can create policies that restrict sign-ins based on location, strength of authentication, and user risk profile.</span></span>

<span data-ttu-id="7b2dc-118">또한 조건부 액세스를 사용하여 Multi-Factor Authentication 정책을 구성하고 사용자 인증에 또 다른 보안 계층을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-118">You can also use conditional access to configure Multi-Factor Authentication policies, adding another layer of security to your user authentications.</span></span> 

### <a name="traffic-termination"></a><span data-ttu-id="7b2dc-119">트래픽 종료</span><span class="sxs-lookup"><span data-stu-id="7b2dc-119">Traffic termination</span></span>

<span data-ttu-id="7b2dc-120">모든 트래픽은 클라우드에서 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-120">All traffic is terminated in the cloud.</span></span>

<span data-ttu-id="7b2dc-121">Azure AD 응용 프로그램 프록시가 역방향 프록시이기 때문에 백 엔드 응용 프로그램으로 전송되는 모든 트래픽은 서비스에서 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-121">Because Azure AD Application Proxy is a reverse-proxy, all traffic to back-end applications is terminated at the service.</span></span> <span data-ttu-id="7b2dc-122">백 엔드 서버에서만 세션을 다시 설정할 수 있습니다. 즉, 백 엔드 서버는 직접 HTTP 트래픽에 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-122">The session can get reestablished only with the back-end server, which means that your back-end servers are not exposed to direct HTTP traffic.</span></span> <span data-ttu-id="7b2dc-123">이 구성은 대상이 지정된 공격으로부터 더 잘 보호받을 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-123">This configuration means that you are better protected from targeted attacks.</span></span>

### <a name="all-access-is-outbound"></a><span data-ttu-id="7b2dc-124">모든 액세스가 아웃바운드임</span><span class="sxs-lookup"><span data-stu-id="7b2dc-124">All access is outbound</span></span> 

<span data-ttu-id="7b2dc-125">회사 네트워크에 대한 인바운드 연결을 열 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-125">You don't need to open inbound connections to the corporate network.</span></span>

<span data-ttu-id="7b2dc-126">응용 프로그램 프록시 커넥터는 Azure AD 응용 프로그램 프록시 서비스에 대한 아웃바운드 연결만 사용하므로 들어오는 연결에 대한 방화벽 포트를 열지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-126">Application Proxy connectors only use outbound connections to the Azure AD Application Proxy service, which means that there is no need to open firewall ports for incoming connections.</span></span> <span data-ttu-id="7b2dc-127">전통적인 프록시에서는 경계 네트워크(*DMZ*, *완충 영역* 또는 *스크린된 서브넷*이라고도 함)가 필요하고 네트워크 에지에서 인증되지 않은 연결에 대한 액세스를 허용해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-127">Traditional proxies required a perimeter network (also known as *DMZ*, *demilitarized zone*, or *screened subnet*) and allowed access to unauthenticated connections at the network edge.</span></span> <span data-ttu-id="7b2dc-128">이 시나리오에서는 트래픽을 분석하고 환경에 추가 보호를 제공하기 위해 웹 응용 프로그램 방화벽 제품에 상당한 투자가 추가로 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-128">This scenario required many additional investments in web application firewall products to analyze traffic and offer addition protections to the environment.</span></span> <span data-ttu-id="7b2dc-129">응용 프로그램 프록시를 사용하는 경우에는 모든 연결은 아웃바운드이고 보안 채널을 통해 발생하기 때문에 경계 네트워크가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-129">With Application Proxy, you don't need a perimeter network because all connections are outbound and take place over a secure channel.</span></span>

<span data-ttu-id="7b2dc-130">커넥터에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-130">For more information about connectors, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

### <a name="cloud-scale-analytics-and-machine-learning"></a><span data-ttu-id="7b2dc-131">클라우드 규모 분석 및 기계 학습</span><span class="sxs-lookup"><span data-stu-id="7b2dc-131">Cloud-scale analytics and machine learning</span></span> 

<span data-ttu-id="7b2dc-132">최첨단 보안 보호를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-132">Get cutting-edge security protection.</span></span>

<span data-ttu-id="7b2dc-133">응용 프로그램 프록시는 Azure Active Directory의 일부이기 때문에 Microsoft Security Response Center 및 Digital Crimes Unit에서 제공하는 기계 학습 기반 인텔리전스 및 데이터를 통해 [Azure AD Identity Protection](active-directory-identityprotection.md)을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-133">Because it's part of Azure Active Directory, Application Proxy can leverage [Azure AD Identity Protection](active-directory-identityprotection.md), with machine learning-driven intelligence and data from the Microsoft Security Response Center and Digital Crimes Unit.</span></span> <span data-ttu-id="7b2dc-134">따라서 손상된 계정을 사전에 식별하고 위험도 높은 로그인으로부터 실시간 보호를 제공합니다. 감염된 장치에서 익명의 네트워크를 통한 액세스, 일반적이고 가능성이 적은 위치 등 다양한 요소를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-134">Together we proactively identify compromised accounts and offer real-time protection from high-risk sign-ins. We take into account numerous factors, such as access from infected devices, through anonymizing networks, and from atypical and unlikely locations.</span></span>

<span data-ttu-id="7b2dc-135">SIEM(보안 정보 및 이벤트 관리) 시스템과 통합을 위해 이러한 많은 보고서 및 이벤트가 API를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-135">Many of these reports and events are already available through an API for integration with your security information and event management (SIEM) systems.</span></span>

### <a name="remote-access-as-a-service"></a><span data-ttu-id="7b2dc-136">서비스로서의 원격 액세스</span><span class="sxs-lookup"><span data-stu-id="7b2dc-136">Remote access as a service</span></span>

<span data-ttu-id="7b2dc-137">온-프레미스 서버의 유지 관리 및 패치 적용에 대해 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-137">You don’t have to worry about maintaining and patching on-premises servers.</span></span>

<span data-ttu-id="7b2dc-138">패치가 적용되지 않은 소프트웨어는 여전히 다수의 공격 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-138">Unpatched software still accounts for a large number of attacks.</span></span> <span data-ttu-id="7b2dc-139">Azure AD 응용 프로그램 프록시는 Microsoft에서 소유하고 있는 인터넷 규모 서비스이므로 항상 최신 보안 패치 및 업그레이드를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-139">Azure AD Application Proxy is an Internet-scale service that Microsoft owns, so you always get the latest security patches and upgrades.</span></span>

<span data-ttu-id="7b2dc-140">Azure AD 응용 프로그램 프록시에 의해 게시된 응용 프로그램의 보안을 개선하기 웹 크롤러 로봇이 응용 프로그램을 인덱싱하고 보관하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-140">To improve the security of applications published by Azure AD Application Proxy, we block web crawler robots from indexing and archiving your applications.</span></span> <span data-ttu-id="7b2dc-141">웹 크롤러 로봇이 게시된 앱에 대한 로봇 설정을 검색하려 할 때마다 응용 프로그램 프록시는 `User-agent: * Disallow: /`를 포함하는 robots.txt 파일로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-141">Each time a web crawler robot tries to retrieve the robot's settings for a published app, Application Proxy replies with a robots.txt file that includes `User-agent: * Disallow: /`.</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="7b2dc-142">내부 살펴보기</span><span class="sxs-lookup"><span data-stu-id="7b2dc-142">Under the hood</span></span>

<span data-ttu-id="7b2dc-143">Azure AD 응용 프로그램 프록시는 두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-143">Azure AD Application Proxy consists of two parts:</span></span>

* <span data-ttu-id="7b2dc-144">클라우드 기반 서비스: Azure에서 실행되며, 외부 클라이언트/사용자를 연결하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-144">The cloud-based service: This service runs in Azure, and is where the external client/user connections are made.</span></span>
* <span data-ttu-id="7b2dc-145">[온-프레미스 커넥터](application-proxy-understand-connectors.md): 온-프레미스 구성 요소인 커넥터는 Azure AD 응용 프로그램 프록시 서비스에서 요청을 수신하고 내부 응용 프로그램에 대한 연결을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-145">[The on-premises connector](application-proxy-understand-connectors.md): An on-premises component, the connector listens for requests from the Azure AD Application Proxy service and handles connections to the internal applications.</span></span> 

<span data-ttu-id="7b2dc-146">커넥터와 응용 프로그램 프록시 서비스 간 흐름은 다음과 같은 경우 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-146">A flow between the connector and the Application Proxy service is established when:</span></span>

* <span data-ttu-id="7b2dc-147">먼저 커넥터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-147">The connector is first set up.</span></span>
* <span data-ttu-id="7b2dc-148">커넥터는 응용 프로그램 프록시 서비스에서 구성 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-148">The connector pulls configuration information from the Application Proxy service.</span></span>
* <span data-ttu-id="7b2dc-149">사용자는 게시된 응용 프로그램에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-149">A user accesses a published application.</span></span>

>[!NOTE]
><span data-ttu-id="7b2dc-150">모든 통신은 SSL을 통해 발생하고 항상 커넥터에서 응용 프로그램 프록시 서비스로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-150">All communications occur over SSL, and they always originate at the connector to the Application Proxy service.</span></span> <span data-ttu-id="7b2dc-151">서비스는 아웃바운드 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-151">The service is outbound only.</span></span>

<span data-ttu-id="7b2dc-152">커넥터는 거의 모든 호출에 대해 응용 프로그램 프록시 서비스를 인증하는 데 클라이언트 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-152">The connector uses a client certificate to authenticate to the Application Proxy service for nearly all calls.</span></span> <span data-ttu-id="7b2dc-153">이 프로세스에 대한 유일한 예외는 클라이언트 인증서가 설정되는 초기 설치 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-153">The only exception to this process is the initial setup step, where the client certificate is established.</span></span>

### <a name="installing-the-connector"></a><span data-ttu-id="7b2dc-154">커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="7b2dc-154">Installing the connector</span></span>

<span data-ttu-id="7b2dc-155">커넥터를 처음 설정할 때 다음과 같은 흐름 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-155">When the connector is first set up, the following flow events take place:</span></span>

1. <span data-ttu-id="7b2dc-156">커넥터 설치 과정의 일부로 서비스에 커넥터 등록이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-156">The connector registration to the service happens as part of the installation of the connector.</span></span> <span data-ttu-id="7b2dc-157">사용자에게 Azure AD 관리자 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-157">Users are prompted to enter their Azure AD admin credentials.</span></span> <span data-ttu-id="7b2dc-158">이 인증에서 얻은 토큰이 Azure AD 응용 프로그램 프록시 서비스에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-158">The token acquired from this authentication is then presented to the Azure AD Application Proxy service.</span></span>
2. <span data-ttu-id="7b2dc-159">응용 프로그램 프록시 서비스에서 토큰을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-159">The Application Proxy service evaluates the token.</span></span> <span data-ttu-id="7b2dc-160">사용자가 토큰을 발급한 테넌트의 회사 관리자임을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-160">It ensures that the user is a company administrator within the tenant that the token was issued for.</span></span> <span data-ttu-id="7b2dc-161">관리자가 아닌 사용자인 경우 프로세스가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-161">If the user is not an administrator, the process is terminated.</span></span>
3. <span data-ttu-id="7b2dc-162">커넥터에서 클라이언트 인증서 요청을 생성하고, 토큰과 함께 이 요청을 응용 프로그램 프록시 서비스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-162">The connector generates a client certificate request and passes it, along with the token, to the Application Proxy service.</span></span> <span data-ttu-id="7b2dc-163">서비스에서 차례로 토큰을 확인하고 클라이언트 인증서 요청에 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-163">The service in turn verifies the token and signs the client certificate request.</span></span>
4. <span data-ttu-id="7b2dc-164">커넥터는 나중에 응용 프로그램 프록시 서비스와 통신하는 데 이 클라이언트 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-164">The connector uses the client certificate for future communication with the Application Proxy service.</span></span>
5. <span data-ttu-id="7b2dc-165">커넥터는 해당 클라이언트 인증서를 사용하여 처음으로 서비스로부터 시스템 구성 데이터 끌어오기를 수행하고 이제 요청을 받을 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-165">The connector performs an initial pull of the system configuration data from the service using its client certificate, and it is now ready to take requests.</span></span>

### <a name="updating-the-configuration-settings"></a><span data-ttu-id="7b2dc-166">구성 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="7b2dc-166">Updating the configuration settings</span></span>

<span data-ttu-id="7b2dc-167">응용 프로그램 프록시 서비스가 구성 설정을 업데이트할 때마다 다음과 같은 흐름 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-167">Whenever the Application Proxy service updates the configuration settings, the following flow events take place:</span></span>

1. <span data-ttu-id="7b2dc-168">커넥터는 해당 클라이언트 인증서를 사용하여 응용 프로그램 프록시 서비스 내의 구성 끝점에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-168">The connector connects to the configuration endpoint within the Application Proxy service by using its client certificate.</span></span>
2. <span data-ttu-id="7b2dc-169">클라이언트 인증서의 유효성을 검사한 후에 응용 프로그램 프록시 서비스가 구성 데이터를 커넥터에 반환합니다. 예를 들어 커넥터가 속하게 될 커넥터 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-169">After the client certificate has been validated, the Application Proxy service returns configuration data to the connector (for example, the connector group that the connector should be part of).</span></span>
3. <span data-ttu-id="7b2dc-170">현재 인증서가 180일 이상 지난 경우 커넥터에서 180일마다 클라이언트 인증서를 효과적으로 업데이트하는 새 인증서 요청을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-170">If the current certificate is more than 180 days old, the connector generates a new certificate request, which effectively updates the client certificate every 180 days.</span></span>

### <a name="accessing-published-applications"></a><span data-ttu-id="7b2dc-171">게시된 응용 프로그램 액세스</span><span class="sxs-lookup"><span data-stu-id="7b2dc-171">Accessing published applications</span></span>

<span data-ttu-id="7b2dc-172">사용자가 게시된 응용 프로그램에 액세스하면 응용 프로그램 프록시 서비스와 응용 프로그램 프록시 커넥터 간에 다음과 같은 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-172">When users access a published application, the following events take place between the Application Proxy service and the Application Proxy connector:</span></span>

1. [<span data-ttu-id="7b2dc-173">서비스가 앱에 대해 사용자를 인증</span><span class="sxs-lookup"><span data-stu-id="7b2dc-173">The service authenticates the user for the app</span></span>](#the-service-checks-the-configuration-settings-for-the-app)
2. [<span data-ttu-id="7b2dc-174">서비스에서 커넥터 큐에 요청 배치</span><span class="sxs-lookup"><span data-stu-id="7b2dc-174">The service places a request in the connector queue</span></span>](#The-service-places-a-request-in-the-connector-queue)
3. [<span data-ttu-id="7b2dc-175">커넥터에서 큐의 요청 처리</span><span class="sxs-lookup"><span data-stu-id="7b2dc-175">A connector processes the request from the queue</span></span>](#the-connector-receives-the-request-from-the-queue)
4. [<span data-ttu-id="7b2dc-176">커넥터에서 응답 대기</span><span class="sxs-lookup"><span data-stu-id="7b2dc-176">The connector waits for a response</span></span>](#the-connector-waits-for-a-response)
5. [<span data-ttu-id="7b2dc-177">서비스에서 사용자에게 데이터 스트리밍</span><span class="sxs-lookup"><span data-stu-id="7b2dc-177">The service streams data to the user</span></span>](#the-service-streams-data-to-the-user)

<span data-ttu-id="7b2dc-178">이러한 단계 각각에서 수행하는 작업에 대해 자세히 알아보려면 계속 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-178">To learn more about what takes place in each of these steps, keep reading.</span></span>


#### <a name="1-the-service-authenticates-the-user-for-the-app"></a><span data-ttu-id="7b2dc-179">1. 서비스가 앱에 대해 사용자를 인증</span><span class="sxs-lookup"><span data-stu-id="7b2dc-179">1. The service authenticates the user for the app</span></span>

<span data-ttu-id="7b2dc-180">사전 인증 방법으로 통과를 사용하도록 앱을 구성한 경우 이 섹션의 단계는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-180">If you configured the app to use Passthrough as its preauthentication method, the steps in this section are skipped.</span></span>

<span data-ttu-id="7b2dc-181">Azure AD를 사용하여 사전 인증하도록 앱을 구성한 경우 사용자는 인증을 위해 Azure AD STS로 리디렉션되고 다음 단계가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-181">If you configured the app to preauthenticate with Azure AD, users are redirected to the Azure AD STS to authenticate, and the following steps take place:</span></span>

1. <span data-ttu-id="7b2dc-182">응용 프로그램 프록시는 특정 응용 프로그램에 대한 조건부 액세스 정책 요구 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-182">Application Proxy checks for any conditional access policy requirements for the specific application.</span></span> <span data-ttu-id="7b2dc-183">이 단계에서는 응용 프로그램에 사용자를 할당했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-183">This step ensures that the user has been assigned to the application.</span></span> <span data-ttu-id="7b2dc-184">2단계 인증이 필요한 경우 인증 시퀀스는 사용자에게 또 다른 인증 방법을 지정하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-184">If two-step verification is required, the authentication sequence prompts the user for a second authentication method.</span></span>

2. <span data-ttu-id="7b2dc-185">모든 확인을 거친 후에 Azure AD STS에서 응용 프로그램에 대해 서명된 토큰을 발급하고 사용자를 다시 응용 프로그램 프록시 서비스로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-185">After all checks have passed, the Azure AD STS issues a signed token for the application and redirects the user back to the Application Proxy service.</span></span>

3. <span data-ttu-id="7b2dc-186">응용 프로그램 프록시는 응용 프로그램을 수정하기 위해 토큰이 발행되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-186">Application Proxy verifies that the token was issued to correct the application.</span></span> <span data-ttu-id="7b2dc-187">토큰이 Azure AD에 의해 서명되었는지, 아직 유효한 기간 내에 있는지를 확인하는 등 다른 확인 작업도 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-187">It performs other checks also, such as ensuring that the token was signed by Azure AD, and that it is still within the valid window.</span></span>

4. <span data-ttu-id="7b2dc-188">응용 프로그램 프록시는 암호화된 인증 쿠키를 설정하여 응용 프로그램에 대한 인증이 발생했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-188">Application Proxy sets an encrypted authentication cookie to indicate that authentication to the application has occurred.</span></span> <span data-ttu-id="7b2dc-189">쿠키에는 Azure AD의 토큰 및 인증 기준이 되는 사용자 이름과 같은 다른 데이터를 기반으로 하는 만료 타임스탬프가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-189">The cookie includes an expiration timestamp that's based on the token from Azure AD and other data, such as the user name that the authentication is based on.</span></span> <span data-ttu-id="7b2dc-190">쿠키는 응용 프로그램 프록시 서비스에만 알려진 개인 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-190">The cookie is encrypted with a private key known only to the Application Proxy service.</span></span>

5. <span data-ttu-id="7b2dc-191">응용 프로그램 프록시는 사용자를 원래 요청된 URL로 다시 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-191">Application Proxy redirects the user back to the originally requested URL.</span></span>

<span data-ttu-id="7b2dc-192">사전 인증 단계 중 일부가 실패하면 사용자 요청이 거부되고 사용자에게 문제 원인을 나타내는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-192">If any part of the preauthentication steps fails, the user’s request is denied, and the user is shown a message indicating the source of the problem.</span></span>


#### <a name="2-the-service-places-a-request-in-the-connector-queue"></a><span data-ttu-id="7b2dc-193">2. 서비스에서 커넥터 큐에 요청 배치</span><span class="sxs-lookup"><span data-stu-id="7b2dc-193">2. The service places a request in the connector queue</span></span>

<span data-ttu-id="7b2dc-194">커넥터에서 응용 프로그램 프록시에 대한 아웃바운드 연결을 열려 있는 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-194">Connectors keep an outbound connection open to the Application Proxy service.</span></span> <span data-ttu-id="7b2dc-195">요청이 들어오면 서비스는 커넥터에서 선택하도록 열려 있는 연결 중 하나에 있는 요청을 큐에 넣습니다</span><span class="sxs-lookup"><span data-stu-id="7b2dc-195">When a request comes in, the service queues up the request on one of the open connections for the connector to pick up.</span></span>

<span data-ttu-id="7b2dc-196">요청에는 요청 헤더, 암호화된 쿠키의 데이터, 요청하는 사용자 및 요청 ID 등 응용 프로그램의 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-196">The request includes items from the application, such as the request headers, data from the encrypted cookie, the user making the request, and the request ID.</span></span> <span data-ttu-id="7b2dc-197">암호화된 쿠키의 데이터가 요청과 함께 전송되지만 인증 쿠키 자체가 전송되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-197">Although data from the encrypted cookie is sent with the request, the authentication cookie itself is not.</span></span>

#### <a name="3-the-connector-processes-the-request-from-the-queue"></a><span data-ttu-id="7b2dc-198">3. 커넥터에서 큐의 요청 처리</span><span class="sxs-lookup"><span data-stu-id="7b2dc-198">3. The connector processes the request from the queue.</span></span> 

<span data-ttu-id="7b2dc-199">요청에 따라 응용 프로그램 프록시는 다음 작업 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-199">Based on the request, Application Proxy performs one of the following actions:</span></span>

* <span data-ttu-id="7b2dc-200">요청이 RESTful *GET* 요청과 함께 그대로 사용하는, 본문 내에 데이터가 없는 것처럼 간단한 작업인 경우 커넥터는 대상 내부 리소스에 대한 연결을 만들고 응답을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-200">If the request is a simple operation (for example, there is no data within the body as is with a RESTful *GET* request), the connector makes a connection to the target internal resource and then waits for a response.</span></span>

* <span data-ttu-id="7b2dc-201">요청에 본문에 있는 내용과 연결된 데이터가 있는 경우(예: RESTful *POST* 작업) 커넥터는 클라이언트 인증서를 사용하여 응용 프로그램 프록시 인스턴스로 아웃바운드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-201">If the request has data associated with it in the body (for example, a RESTful *POST* operation), the connector makes an outbound connection by using the client certificate to the Application Proxy instance.</span></span> <span data-ttu-id="7b2dc-202">이 연결을 만들어서 데이터를 요청하고 내부 리소스에 대한 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-202">It makes this connection to request the data and open a connection to the internal resource.</span></span> <span data-ttu-id="7b2dc-203">커넥터에서 요청을 받은 후에 응용 프로그램 프록시 서비스는 사용자로부터 콘텐츠를 수락하고 데이터를 커넥터에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-203">After it receives the request from the connector, the Application Proxy service begins accepting content from the user and forwards data to the connector.</span></span> <span data-ttu-id="7b2dc-204">그러면 커넥터가 데이터를 내부 리소스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-204">The connector, in turn, forwards the data to the internal resource.</span></span>

#### <a name="4-the-connector-waits-for-a-response"></a><span data-ttu-id="7b2dc-205">4. 커넥터에서 응답 대기</span><span class="sxs-lookup"><span data-stu-id="7b2dc-205">4. The connector waits for a response.</span></span>

<span data-ttu-id="7b2dc-206">백 엔드로 모든 콘텐츠의 요청 및 전송이 완료된 후에 커넥터가 응답을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-206">After the request and transmission of all content to the back end is complete, the connector waits for a response.</span></span>

<span data-ttu-id="7b2dc-207">응답이 수신된 후에 커넥터가 응용 프로그램 프록시 서비스로 아웃바운드 연결을 만들어 헤더 세부 정보를 반환하고 반환 데이터의 스트리밍을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-207">After it receives a response, the connector makes an outbound connection to the Application Proxy service, to return the header details and begin streaming the return data.</span></span>

#### <a name="5-the-service-streams-data-to-the-user"></a><span data-ttu-id="7b2dc-208">5. 서비스에서 사용자에게 데이터 스트리밍</span><span class="sxs-lookup"><span data-stu-id="7b2dc-208">5. The service streams data to the user.</span></span> 

<span data-ttu-id="7b2dc-209">응용 프로그램의 처리 일부가 여기서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-209">Some processing of the application may occur here.</span></span> <span data-ttu-id="7b2dc-210">응용 프로그램에서 헤더 또는 URL을 변환하도록 응용 프로그램 프록시를 구성한 경우 이 단계에서 필요에 따라 해당 처리가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b2dc-210">If you configured Application Proxy to translate headers or URLs in your application, that processing happens as needed during this step.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7b2dc-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b2dc-211">Next steps</span></span>

[<span data-ttu-id="7b2dc-212">Azure AD 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항</span><span class="sxs-lookup"><span data-stu-id="7b2dc-212">Network topology considerations when using Azure AD Application Proxy</span></span>](application-proxy-network-topology-considerations.md)

[<span data-ttu-id="7b2dc-213">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="7b2dc-213">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
