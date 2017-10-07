---
title: "Azure AD 응용 프로그램 프록시에 대 한 고려 사항 aaaSecurity | Microsoft Docs"
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
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a><span data-ttu-id="c758f-103">Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="c758f-103">Security considerations for accessing apps remotely with Azure AD Application Proxy</span></span>

<span data-ttu-id="c758f-104">이 문서에서는 Azure Active Directory 응용 프로그램 프록시 서비스에서 응용 프로그램을 원격으로 게시 및 액세스하기 위한 안전한 서비스를 제공하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-104">This article explains how Azure Active Directory Application Proxy provides a secure service for publishing and accessing your applications remotely.</span></span>

<span data-ttu-id="c758f-105">다음 다이어그램에 표시 방법을 Azure AD는 hello를 사용 하면 보안 된 원격 액세스 tooyour 온-프레미스 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-105">hello following diagram shows how Azure AD enables secure remote access tooyour on-premises applications.</span></span>

 ![Azure AD 응용 프로그램 프록시를 통한 보안 원격 액세스의 다이어그램](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a><span data-ttu-id="c758f-107">보안 이점</span><span class="sxs-lookup"><span data-stu-id="c758f-107">Security benefits</span></span>

<span data-ttu-id="c758f-108">Azure AD 응용 프로그램 프록시는 hello 다음 보안 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-108">Azure AD Application Proxy offers hello following security benefits:</span></span>

### <a name="authenticated-access"></a><span data-ttu-id="c758f-109">인증된 액세스</span><span class="sxs-lookup"><span data-stu-id="c758f-109">Authenticated access</span></span> 

<span data-ttu-id="c758f-110">Toouse Azure Active Directory 사전 인증을 선택 하면 인증 된 연결만 네트워크에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-110">If you choose toouse Azure Active Directory preauthentication, then only authenticated connections can access your network.</span></span>

<span data-ttu-id="c758f-111">Azure AD 응용 프로그램 프록시는 hello 모든 인증의 Azure AD 보안 토큰 서비스 (STS)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-111">Azure AD Application Proxy relies on hello Azure AD security token service (STS) for all authentication.</span></span>  <span data-ttu-id="c758f-112">사전 인증을은 본질적으로 차단 익명 공격 상당수 인증 된 id만 hello 백 엔드 응용 프로그램에 액세스할 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-112">Preauthentication, by its very nature, blocks a significant number of anonymous attacks, because only authenticated identities can access hello back-end application.</span></span>

<span data-ttu-id="c758f-113">사전 인증 방법으로 통과를 선택하면 이러한 이점을 활용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-113">If you choose Passthrough as your preauthentication method, you don't get this benefit.</span></span> 

### <a name="conditional-access"></a><span data-ttu-id="c758f-114">조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="c758f-114">Conditional access</span></span>

<span data-ttu-id="c758f-115">Tooyour 네트워크 설정 된 연결 하기 전에 다양 한 정책 제어를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-115">Apply richer policy controls before connections tooyour network are established.</span></span>

<span data-ttu-id="c758f-116">와 [조건부 액세스](active-directory-conditional-access-azuread-connected-apps.md)를 정의할 수 있습니다 트래픽 종류에 대 한 제한이 tooaccess 백 엔드 응용 프로그램을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-116">With [conditional access](active-directory-conditional-access-azuread-connected-apps.md), you can define restrictions on what traffic is allowed tooaccess your back-end applications.</span></span> <span data-ttu-id="c758f-117">위치, 인증 강도 및 사용자 위험 프로필에 따라 로그인을 제한하는 정책을 사항을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-117">You can create policies that restrict sign-ins based on location, strength of authentication, and user risk profile.</span></span>

<span data-ttu-id="c758f-118">또한 보안 tooyour 사용자 인증의 다른 레이어를 추가 조건부 액세스 tooconfigure Multi-factor Authentication 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-118">You can also use conditional access tooconfigure Multi-Factor Authentication policies, adding another layer of security tooyour user authentications.</span></span> 

### <a name="traffic-termination"></a><span data-ttu-id="c758f-119">트래픽 종료</span><span class="sxs-lookup"><span data-stu-id="c758f-119">Traffic termination</span></span>

<span data-ttu-id="c758f-120">모든 트래픽이 hello 클라우드에서 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-120">All traffic is terminated in hello cloud.</span></span>

<span data-ttu-id="c758f-121">Azure AD 응용 프로그램 프록시는 역방향 프록시 이기 때문에 모든 트래픽 tooback 간 응용 프로그램은 hello 서비스에서 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-121">Because Azure AD Application Proxy is a reverse-proxy, all traffic tooback-end applications is terminated at hello service.</span></span> <span data-ttu-id="c758f-122">hello 세션 가져올 다시 설정할 수 있는 hello 백 엔드 서버에만 백 엔드 서버에 없는 즉 toodirect HTTP 트래픽을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-122">hello session can get reestablished only with hello back-end server, which means that your back-end servers are not exposed toodirect HTTP traffic.</span></span> <span data-ttu-id="c758f-123">이 구성은 대상이 지정된 공격으로부터 더 잘 보호받을 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-123">This configuration means that you are better protected from targeted attacks.</span></span>

### <a name="all-access-is-outbound"></a><span data-ttu-id="c758f-124">모든 액세스가 아웃바운드임</span><span class="sxs-lookup"><span data-stu-id="c758f-124">All access is outbound</span></span> 

<span data-ttu-id="c758f-125">Tooopen 인바운드 연결 toohello 회사 네트워크가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-125">You don't need tooopen inbound connections toohello corporate network.</span></span>

<span data-ttu-id="c758f-126">응용 프로그램 프록시 커넥터는만 있다는 것을 의미 하지 않아도 tooopen 방화벽 포트 들어오는 연결에 대 한 아웃 바운드 연결 toohello Azure AD 응용 프로그램 프록시 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-126">Application Proxy connectors only use outbound connections toohello Azure AD Application Proxy service, which means that there is no need tooopen firewall ports for incoming connections.</span></span> <span data-ttu-id="c758f-127">기존 프록시 필요한 경계 네트워크 (라고도 *DMZ*, *완충 영역*, 또는 *스크린 된 서브넷*) toounauthenticated 액세스 허용 hello 네트워크 가장자리에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-127">Traditional proxies required a perimeter network (also known as *DMZ*, *demilitarized zone*, or *screened subnet*) and allowed access toounauthenticated connections at hello network edge.</span></span> <span data-ttu-id="c758f-128">이 시나리오는 웹 응용 프로그램에서 추가 투자가 많은 제품 tooanalyze 트래픽이 방화벽 및 추가 보호 기능은 toohello 환경을 제공 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-128">This scenario required many additional investments in web application firewall products tooanalyze traffic and offer addition protections toohello environment.</span></span> <span data-ttu-id="c758f-129">응용 프로그램 프록시를 사용하는 경우에는 모든 연결은 아웃바운드이고 보안 채널을 통해 발생하기 때문에 경계 네트워크가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-129">With Application Proxy, you don't need a perimeter network because all connections are outbound and take place over a secure channel.</span></span>

<span data-ttu-id="c758f-130">커넥터에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c758f-130">For more information about connectors, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

### <a name="cloud-scale-analytics-and-machine-learning"></a><span data-ttu-id="c758f-131">클라우드 규모 분석 및 기계 학습</span><span class="sxs-lookup"><span data-stu-id="c758f-131">Cloud-scale analytics and machine learning</span></span> 

<span data-ttu-id="c758f-132">최첨단 보안 보호를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-132">Get cutting-edge security protection.</span></span>

<span data-ttu-id="c758f-133">Azure Active Directory의 일부 이기 때문에 응용 프로그램 프록시를 활용해 [Azure AD Identity Protection](active-directory-identityprotection.md), 컴퓨터 학습 기반 인텔리전스 및 Microsoft 보안 대응 센터 hello 및 Digital Crimes Unit에서 데이터와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-133">Because it's part of Azure Active Directory, Application Proxy can leverage [Azure AD Identity Protection](active-directory-identityprotection.md), with machine learning-driven intelligence and data from hello Microsoft Security Response Center and Digital Crimes Unit.</span></span> <span data-ttu-id="c758f-134">따라서 손상된 계정을 사전에 식별하고 위험도 높은 로그인으로부터 실시간 보호를 제공합니다. 감염된 장치에서 익명의 네트워크를 통한 액세스, 일반적이고 가능성이 적은 위치 등 다양한 요소를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-134">Together we proactively identify compromised accounts and offer real-time protection from high-risk sign-ins. We take into account numerous factors, such as access from infected devices, through anonymizing networks, and from atypical and unlikely locations.</span></span>

<span data-ttu-id="c758f-135">SIEM(보안 정보 및 이벤트 관리) 시스템과 통합을 위해 이러한 많은 보고서 및 이벤트가 API를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-135">Many of these reports and events are already available through an API for integration with your security information and event management (SIEM) systems.</span></span>

### <a name="remote-access-as-a-service"></a><span data-ttu-id="c758f-136">서비스로서의 원격 액세스</span><span class="sxs-lookup"><span data-stu-id="c758f-136">Remote access as a service</span></span>

<span data-ttu-id="c758f-137">유지 관리 하 고 온-프레미스 서버를 패치 하는 방법에 대 한 tooworry가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-137">You don’t have tooworry about maintaining and patching on-premises servers.</span></span>

<span data-ttu-id="c758f-138">패치가 적용되지 않은 소프트웨어는 여전히 다수의 공격 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-138">Unpatched software still accounts for a large number of attacks.</span></span> <span data-ttu-id="c758f-139">Azure AD 응용 프로그램 프록시 Microsoft 소유 하는 인터넷 범위의 서비스 이므로 hello 최신 보안 패치 및 업그레이드를 항상에 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-139">Azure AD Application Proxy is an Internet-scale service that Microsoft owns, so you always get hello latest security patches and upgrades.</span></span>

<span data-ttu-id="c758f-140">Azure AD 응용 프로그램 프록시에 의해 게시 된 응용 프로그램의 tooimprove hello 보안, 인덱싱 및 응용 프로그램 보관에서 웹 크롤러 로봇 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-140">tooimprove hello security of applications published by Azure AD Application Proxy, we block web crawler robots from indexing and archiving your applications.</span></span> <span data-ttu-id="c758f-141">웹 크롤러 로봇이 게시된 앱에 대한 로봇 설정을 검색하려 할 때마다 응용 프로그램 프록시는 `User-agent: * Disallow: /`를 포함하는 robots.txt 파일로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-141">Each time a web crawler robot tries to retrieve the robot's settings for a published app, Application Proxy replies with a robots.txt file that includes `User-agent: * Disallow: /`.</span></span>

## <a name="under-hello-hood"></a><span data-ttu-id="c758f-142">Hello 내부적</span><span class="sxs-lookup"><span data-stu-id="c758f-142">Under hello hood</span></span>

<span data-ttu-id="c758f-143">Azure AD 응용 프로그램 프록시는 두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-143">Azure AD Application Proxy consists of two parts:</span></span>

* <span data-ttu-id="c758f-144">클라우드 기반 서비스 hello:이 서비스를 Azure에서 실행에 대 한 hello 외부 클라이언트/사용자 연결은 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-144">hello cloud-based service: This service runs in Azure, and is where hello external client/user connections are made.</span></span>
* <span data-ttu-id="c758f-145">[hello 온-프레미스 커넥터](application-proxy-understand-connectors.md): hello 커넥터는 온-프레미스 구성 요소, hello Azure AD 응용 프로그램 프록시 서비스에서 요청을 수신 하 고 연결 toohello 내부 응용 프로그램을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-145">[hello on-premises connector](application-proxy-understand-connectors.md): An on-premises component, hello connector listens for requests from hello Azure AD Application Proxy service and handles connections toohello internal applications.</span></span> 

<span data-ttu-id="c758f-146">Hello 커넥터와 hello 응용 프로그램 프록시 서비스 간의 흐름 설정 되는 경우:</span><span class="sxs-lookup"><span data-stu-id="c758f-146">A flow between hello connector and hello Application Proxy service is established when:</span></span>

* <span data-ttu-id="c758f-147">hello 커넥터 처음 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-147">hello connector is first set up.</span></span>
* <span data-ttu-id="c758f-148">hello 커넥터 hello 응용 프로그램 프록시 서비스에서에서 구성 정보를 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-148">hello connector pulls configuration information from hello Application Proxy service.</span></span>
* <span data-ttu-id="c758f-149">사용자는 게시된 응용 프로그램에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-149">A user accesses a published application.</span></span>

>[!NOTE]
><span data-ttu-id="c758f-150">모든 통신은 SSL을 통해 발생 하 고 항상 hello 커넥터 toohello 응용 프로그램 프록시 서비스에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-150">All communications occur over SSL, and they always originate at hello connector toohello Application Proxy service.</span></span> <span data-ttu-id="c758f-151">hello 서비스는 아웃 바운드만 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-151">hello service is outbound only.</span></span>

<span data-ttu-id="c758f-152">hello 커넥터는 클라이언트 인증서 tooauthenticate toohello 거의 모든 호출에 대 한 응용 프로그램 프록시 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-152">hello connector uses a client certificate tooauthenticate toohello Application Proxy service for nearly all calls.</span></span> <span data-ttu-id="c758f-153">hello만 예외 toothis 프로세스는 hello 초기 설치 단계 hello 클라이언트 인증서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-153">hello only exception toothis process is hello initial setup step, where hello client certificate is established.</span></span>

### <a name="installing-hello-connector"></a><span data-ttu-id="c758f-154">Hello 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="c758f-154">Installing hello connector</span></span>

<span data-ttu-id="c758f-155">Hello 커넥터를 처음 설치할 때 다음 흐름 이벤트 hello 수행.</span><span class="sxs-lookup"><span data-stu-id="c758f-155">When hello connector is first set up, hello following flow events take place:</span></span>

1. <span data-ttu-id="c758f-156">hello 커넥터 등록 toohello 서비스는 hello 커넥터의 hello 설치 과정의 일환으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-156">hello connector registration toohello service happens as part of hello installation of hello connector.</span></span> <span data-ttu-id="c758f-157">사용자가 자신의 Azure AD 관리자 자격 증명된 tooenter 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-157">Users are prompted tooenter their Azure AD admin credentials.</span></span> <span data-ttu-id="c758f-158">이 인증에서 가져온 토큰 toohello Azure AD 응용 프로그램 프록시 서비스를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-158">The token acquired from this authentication is then presented toohello Azure AD Application Proxy service.</span></span>
2. <span data-ttu-id="c758f-159">hello 응용 프로그램 프록시 서비스는 hello 토큰을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-159">hello Application Proxy service evaluates hello token.</span></span> <span data-ttu-id="c758f-160">Hello 사용자가 토큰 hello hello 테 넌 트 내에서 회사 관리자에 대해 실행 되었습니다 되도록 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-160">It ensures that hello user is a company administrator within hello tenant that hello token was issued for.</span></span> <span data-ttu-id="c758f-161">Hello 사용자가 관리자가 아닌 hello 프로세스가 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-161">If hello user is not an administrator, hello process is terminated.</span></span>
3. <span data-ttu-id="c758f-162">hello 커넥터는 클라이언트 인증서 요청을 생성 하 고 hello 토큰, toohello 응용 프로그램 프록시 서비스와 함께 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-162">hello connector generates a client certificate request and passes it, along with hello token, toohello Application Proxy service.</span></span> <span data-ttu-id="c758f-163">그러면 hello 서비스는 hello 토큰을 확인 하 고 hello 클라이언트 인증서 요청에 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-163">hello service in turn verifies hello token and signs hello client certificate request.</span></span>
4. <span data-ttu-id="c758f-164">hello 커넥터 응용 프로그램 프록시 서비스 hello로 나중에 통신에 대 한 hello 클라이언트 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-164">hello connector uses hello client certificate for future communication with hello Application Proxy service.</span></span>
5. <span data-ttu-id="c758f-165">hello 커넥터에서 해당 클라이언트 인증서를 사용 하 여 hello 서비스 hello 시스템 구성 데이터의 초기는 끌어오기를 수행 하 고 준비 tootake 요청 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-165">hello connector performs an initial pull of hello system configuration data from hello service using its client certificate, and it is now ready tootake requests.</span></span>

### <a name="updating-hello-configuration-settings"></a><span data-ttu-id="c758f-166">Hello 구성 설정을 업데이트</span><span class="sxs-lookup"><span data-stu-id="c758f-166">Updating hello configuration settings</span></span>

<span data-ttu-id="c758f-167">Hello 구성 설정을 업데이트 하는 응용 프로그램 프록시 서비스 hello, 때마다 hello 흐름 이벤트 뒤 수행.</span><span class="sxs-lookup"><span data-stu-id="c758f-167">Whenever hello Application Proxy service updates hello configuration settings, hello following flow events take place:</span></span>

1. <span data-ttu-id="c758f-168">해당 클라이언트 인증서를 사용 하 여 hello 응용 프로그램 프록시 서비스 내에서 toohello 구성 끝점을 연결 하는 hello 연결선입니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-168">hello connector connects toohello configuration endpoint within hello Application Proxy service by using its client certificate.</span></span>
2. <span data-ttu-id="c758f-169">Hello 응용 프로그램 프록시 서비스 구성 데이터 toohello 커넥터 반환 hello 클라이언트 인증서를 확인 한 후 (예를 들어 커넥터 hello hello 커넥터 그룹의 일부 여야) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-169">After hello client certificate has been validated, hello Application Proxy service returns configuration data toohello connector (for example, hello connector group that hello connector should be part of).</span></span>
3. <span data-ttu-id="c758f-170">Hello 현재 인증서 180 일 이상 이전 이면 hello 커넥터가 효과적으로 180 일 마다 hello 클라이언트 인증서를 업데이트 하는 새 인증서 요청을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-170">If hello current certificate is more than 180 days old, hello connector generates a new certificate request, which effectively updates hello client certificate every 180 days.</span></span>

### <a name="accessing-published-applications"></a><span data-ttu-id="c758f-171">게시된 응용 프로그램 액세스</span><span class="sxs-lookup"><span data-stu-id="c758f-171">Accessing published applications</span></span>

<span data-ttu-id="c758f-172">사용자가 게시 된 응용 프로그램에 액세스 하는 경우 hello 다음과 같은 이벤트가 수행 hello 응용 프로그램 프록시 서비스와 응용 프로그램 프록시 커넥터 hello 사이.</span><span class="sxs-lookup"><span data-stu-id="c758f-172">When users access a published application, hello following events take place between hello Application Proxy service and hello Application Proxy connector:</span></span>

1. [<span data-ttu-id="c758f-173">hello 서비스 hello 앱에 대 한 hello 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-173">hello service authenticates hello user for hello app</span></span>](#the-service-checks-the-configuration-settings-for-the-app)
2. [<span data-ttu-id="c758f-174">hello 서비스는 hello 커넥터 큐에 요청을 전달</span><span class="sxs-lookup"><span data-stu-id="c758f-174">hello service places a request in hello connector queue</span></span>](#The-service-places-a-request-in-the-connector-queue)
3. [<span data-ttu-id="c758f-175">Hello 큐에서 hello 요청을 처리 하는 커넥터</span><span class="sxs-lookup"><span data-stu-id="c758f-175">A connector processes hello request from hello queue</span></span>](#the-connector-receives-the-request-from-the-queue)
4. [<span data-ttu-id="c758f-176">응답을 대기 하는 hello 커넥터</span><span class="sxs-lookup"><span data-stu-id="c758f-176">hello connector waits for a response</span></span>](#the-connector-waits-for-a-response)
5. [<span data-ttu-id="c758f-177">hello 서비스 스트림 데이터 toohello 사용자</span><span class="sxs-lookup"><span data-stu-id="c758f-177">hello service streams data toohello user</span></span>](#the-service-streams-data-to-the-user)

<span data-ttu-id="c758f-178">이러한 단계를 각각 수행 기능에 대 한 자세한 toolearn 계속 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-178">toolearn more about what takes place in each of these steps, keep reading.</span></span>


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a><span data-ttu-id="c758f-179">1. hello 서비스 hello 앱에 대 한 hello 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-179">1. hello service authenticates hello user for hello app</span></span>

<span data-ttu-id="c758f-180">Hello 앱 toouse 통과 사전 인증 방법으로 구성한 경우이 섹션의 hello 단계는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-180">If you configured hello app toouse Passthrough as its preauthentication method, hello steps in this section are skipped.</span></span>

<span data-ttu-id="c758f-181">Azure AD와 앱 toopreauthenticate hello를 구성한 경우 사용자가 Azure AD STS tooauthenticate 리디렉션된 toohello 및 hello 다음 단계가 수행:</span><span class="sxs-lookup"><span data-stu-id="c758f-181">If you configured hello app toopreauthenticate with Azure AD, users are redirected toohello Azure AD STS tooauthenticate, and hello following steps take place:</span></span>

1. <span data-ttu-id="c758f-182">응용 프로그램 프록시 hello 특정 응용 프로그램에 대 한 조건부 액세스 정책 요구 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-182">Application Proxy checks for any conditional access policy requirements for hello specific application.</span></span> <span data-ttu-id="c758f-183">이렇게 하면 해당 hello 사용자 toohello 응용 프로그램에 할당 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-183">This step ensures that hello user has been assigned toohello application.</span></span> <span data-ttu-id="c758f-184">2 단계 인증을 필요한 경우 hello 인증 시퀀스 메시지는 두 번째 인증 방법에 대 한 hello 사용자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-184">If two-step verification is required, hello authentication sequence prompts hello user for a second authentication method.</span></span>

2. <span data-ttu-id="c758f-185">모든 검사에 통과 했음을, 후 hello Azure AD STS hello 응용 프로그램에 대 한 서명 된 토큰을 발급 하 고 리디렉션을 hello 사용자 백 toohello 응용 프로그램 프록시 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-185">After all checks have passed, hello Azure AD STS issues a signed token for hello application and redirects hello user back toohello Application Proxy service.</span></span>

3. <span data-ttu-id="c758f-186">응용 프로그램 프록시 hello 토큰 발급 toocorrect hello 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-186">Application Proxy verifies that hello token was issued toocorrect hello application.</span></span> <span data-ttu-id="c758f-187">또한 다른 검사를 수행 하 고 해당 hello 시키는 토큰 Azure AD를 사용 하 여 서명 hello 유효한 창 내에 있는 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-187">It performs other checks also, such as ensuring that hello token was signed by Azure AD, and that it is still within hello valid window.</span></span>

4. <span data-ttu-id="c758f-188">응용 프로그램 프록시는 암호화 된 인증 쿠키 tooindicate toohello 응용 프로그램 인증 발생 했음을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-188">Application Proxy sets an encrypted authentication cookie tooindicate that authentication toohello application has occurred.</span></span> <span data-ttu-id="c758f-189">hello 쿠키 포함 Azure AD의 토큰을 hello 및 기타 데이터를 기반으로 하는 만료 타임 스탬프 인증 hello hello 사용자 이름을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-189">hello cookie includes an expiration timestamp that's based on hello token from Azure AD and other data, such as hello user name that hello authentication is based on.</span></span> <span data-ttu-id="c758f-190">hello 쿠키 toohello 응용 프로그램 프록시 서비스를 알고 있는 개인 키로 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-190">hello cookie is encrypted with a private key known only toohello Application Proxy service.</span></span>

5. <span data-ttu-id="c758f-191">응용 프로그램 프록시 리디렉션을 hello 사용자 백 toohello는 원래 URL을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-191">Application Proxy redirects hello user back toohello originally requested URL.</span></span>

<span data-ttu-id="c758f-192">Hello 사전 인증 단계의 일부가 실패 하면, hello 사용자의 요청이 거부 되 면 하 고 hello 사용자 hello 문제의 hello 원인을 나타내는 메시지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-192">If any part of hello preauthentication steps fails, hello user’s request is denied, and hello user is shown a message indicating hello source of hello problem.</span></span>


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a><span data-ttu-id="c758f-193">2. hello 서비스는 hello 커넥터 큐에 요청을 전달</span><span class="sxs-lookup"><span data-stu-id="c758f-193">2. hello service places a request in hello connector queue</span></span>

<span data-ttu-id="c758f-194">커넥터는 아웃 바운드 연결 열기 toohello 응용 프로그램 프록시 서비스를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-194">Connectors keep an outbound connection open toohello Application Proxy service.</span></span> <span data-ttu-id="c758f-195">대 한 요청이 들어오면 hello 서비스 hello 커넥터 toopick hello에 대 한 열린 연결 중 하나에서 hello 요청을 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-195">When a request comes in, hello service queues up hello request on one of hello open connections for hello connector toopick up.</span></span>

<span data-ttu-id="c758f-196">hello 요청 헤더와 데이터를 암호화 하는 hello 쿠키 같은 hello 응용 프로그램에서 항목을 포함 하는 hello 요청, 요청을 hello 고 hello hello 사용자를 만드는 요청 id입니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-196">hello request includes items from hello application, such as hello request headers, data from hello encrypted cookie, hello user making hello request, and hello request ID.</span></span> <span data-ttu-id="c758f-197">Hello 암호화 된 쿠키에서 데이터는 hello 요청으로 전송 하지만 hello 인증 쿠키와 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-197">Although data from hello encrypted cookie is sent with hello request, hello authentication cookie itself is not.</span></span>

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a><span data-ttu-id="c758f-198">3. hello 커넥터 hello 큐에서 hello 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-198">3. hello connector processes hello request from hello queue.</span></span> 

<span data-ttu-id="c758f-199">Hello 요청에 따라 응용 프로그램 프록시 중 하나를 수행 작업을 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="c758f-199">Based on hello request, Application Proxy performs one of hello following actions:</span></span>

* <span data-ttu-id="c758f-200">Hello 요청은 간단한 작업 하는 경우 (예를 들어 RESTful는 있는 그대로 hello 본문 내에서 데이터가 없는 *가져오기* 요청), hello 커넥터 연결 toohello 대상 내부 리소스를 만들고 다음 응답을 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-200">If hello request is a simple operation (for example, there is no data within hello body as is with a RESTful *GET* request), hello connector makes a connection toohello target internal resource and then waits for a response.</span></span>

* <span data-ttu-id="c758f-201">Hello 요청에 데이터 hello 본문에 연결 된 경우 (RESTful 예를 들어 *POST* 작업), hello 커넥터 hello 클라이언트 인증서 toohello 응용 프로그램 프록시 인스턴스를 사용 하 여 아웃 바운드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-201">If hello request has data associated with it in hello body (for example, a RESTful *POST* operation), hello connector makes an outbound connection by using hello client certificate toohello Application Proxy instance.</span></span> <span data-ttu-id="c758f-202">이 연결 toorequest hello 데이터 있도록 지정 하 고 연결 toohello 내부 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-202">It makes this connection toorequest hello data and open a connection toohello internal resource.</span></span> <span data-ttu-id="c758f-203">Hello 요청 hello 커넥터에서 수신한 후 hello 응용 프로그램 프록시 서비스는 hello 사용자의 콘텐츠를 수락을 시작 하 고 데이터 toohello 커넥터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-203">After it receives hello request from hello connector, hello Application Proxy service begins accepting content from hello user and forwards data toohello connector.</span></span> <span data-ttu-id="c758f-204">hello 커넥터 차례로 hello 데이터 toohello 내부 리소스를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-204">hello connector, in turn, forwards hello data toohello internal resource.</span></span>

#### <a name="4-hello-connector-waits-for-a-response"></a><span data-ttu-id="c758f-205">4. hello 커넥터 응답을 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-205">4. hello connector waits for a response.</span></span>

<span data-ttu-id="c758f-206">Hello 요청 및 모든 콘텐츠 toohello의 전송을 다시 후에 최종 완료 되 면 hello 커넥터 응답을 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-206">After hello request and transmission of all content toohello back end is complete, hello connector waits for a response.</span></span>

<span data-ttu-id="c758f-207">응답을 수신한 후 hello 커넥터에서 아웃 바운드 연결 toohello 응용 프로그램 프록시 서비스를 사용 하면, tooreturn hello 헤더 정보 및 스트리밍 hello 반환 데이터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-207">After it receives a response, hello connector makes an outbound connection toohello Application Proxy service, tooreturn hello header details and begin streaming hello return data.</span></span>

#### <a name="5-hello-service-streams-data-toohello-user"></a><span data-ttu-id="c758f-208">5. hello 서비스 스트림 데이터 toohello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-208">5. hello service streams data toohello user.</span></span> 

<span data-ttu-id="c758f-209">여기에 일부 처리 hello 응용 프로그램의 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-209">Some processing of hello application may occur here.</span></span> <span data-ttu-id="c758f-210">응용 프로그램에서 응용 프로그램 프록시 tootranslate 헤더 또는 Url을 구성한 경우이 단계 동안 필요에 따라 해당 처리가 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="c758f-210">If you configured Application Proxy tootranslate headers or URLs in your application, that processing happens as needed during this step.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c758f-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c758f-211">Next steps</span></span>

[<span data-ttu-id="c758f-212">Azure AD 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항</span><span class="sxs-lookup"><span data-stu-id="c758f-212">Network topology considerations when using Azure AD Application Proxy</span></span>](application-proxy-network-topology-considerations.md)

[<span data-ttu-id="c758f-213">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="c758f-213">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
