---
title: "온-프레미스 앱에 대한 보안된 원격 액세스를 제공하는 방법"
description: "Azure AD 응용 프로그램 프록시를 사용하여 온-프레미스 앱에 대한 보안된 원격 액세스를 제공하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 67f7f5b8d411d11c97a8666d1bfc3c0c5f1174ce
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-provide-secure-remote-access-to-on-premises-applications"></a><span data-ttu-id="5be89-103">온-프레미스 응용 프로그램에 보안된 원격 액세스를 제공하는 방법</span><span class="sxs-lookup"><span data-stu-id="5be89-103">How to provide secure remote access to on-premises applications</span></span>

<span data-ttu-id="5be89-104">요즈음 직원은 어디서나 언제든지 어느 장치에서나 생산성을 높이기를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-104">Employees today want to be productive at any place, at any time, and from any device.</span></span> <span data-ttu-id="5be89-105">태블릿, 휴대폰 또는 랩톱을 막론하고 자신의 장치에서 일하기를 원합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-105">They want to work on their own devices, whether they be tablets, phones, or laptops.</span></span> <span data-ttu-id="5be89-106">그리고 해당하는 모든 응용 프로그램인 클라우드의 SaaS 앱 및 회사 앱 온-프레미스 모두에도 액세스할 수 있다고 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-106">And they expect to be able to access all their applications, both SaaS apps in the cloud and corporate apps on-premises.</span></span> <span data-ttu-id="5be89-107">온-프레미스 응용 프로그램에 대한 액세스를 제공하려면 일반적으로 가상 사설망(VPN) 또는 완충 영역(DMZ)이 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-107">Providing access to on-premises applications has traditionally involved virtual private networks (VPNs) or demilitarized zones (DMZs).</span></span> <span data-ttu-id="5be89-108">이러한 솔루션은 복잡하고 안전하게 만들기도 어려울 뿐만 아니라 설정과 관리에도 비용이 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-108">Not only are these solutions complex and hard to make secure, but they are costly to set up and manage.</span></span>

<span data-ttu-id="5be89-109">더 나은 방법이 있습니다!</span><span class="sxs-lookup"><span data-stu-id="5be89-109">There is a better way!</span></span>

<span data-ttu-id="5be89-110">모바일 중심, 클라우드 중심의 최신 인력에게는 최신 원격 액세스 솔루션을 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-110">A modern workforce in the mobile-first, cloud-first world needs a modern remote access solution.</span></span> <span data-ttu-id="5be89-111">Azure AD 응용 프로그램 프록시는 Azure Active Directory의 기능이며 원격 액세스 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-111">Azure AD Application Proxy is a feature of Azure Active Directory that offers remote access as a service.</span></span> <span data-ttu-id="5be89-112">즉, 배포, 사용 및 관리하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-112">That means it's easy to deploy, use, and manage.</span></span>

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a><span data-ttu-id="5be89-113">Azure Active Directory 응용 프로그램 프록시란?</span><span class="sxs-lookup"><span data-stu-id="5be89-113">What is Azure Active Directory Application Proxy?</span></span>
<span data-ttu-id="5be89-114">Azure AD 응용 프로그램 프록시는 온-프레미스에 호스트된 웹 응용 프로그램에 대한 SSO(Single Sign-On) 및 보안된 원격 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-114">Azure AD Application Proxy provides single sign-on (SSO) and secure remote access for web applications hosted on-premises.</span></span> <span data-ttu-id="5be89-115">게시하려는 일부 앱은 SharePoint 사이트, Outlook Web Access 또는 사용자가 가지고 있는 다른 LOB 웹 응용 프로그램을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-115">Some apps you would want to publish include SharePoint sites, Outlook Web Access, or any other LOB web applications you have.</span></span> <span data-ttu-id="5be89-116">이러한 온-프레미스 웹 응용 프로그램은 Azure AD, 동일한 ID 및 O365에서 사용되는 제어 플랫폼과 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-116">These on-premises web applications are integrated with Azure AD, the same identity and control platform that is used by O365.</span></span> <span data-ttu-id="5be89-117">최종 사용자는 O365 및 Azure AD와 통합된 다른 SaaS 앱에 액세스할 때와 같은 방식으로 온-프레미스 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-117">End users can access your on-premises applications the same way they access O365 and other SaaS apps integrated with Azure AD.</span></span> <span data-ttu-id="5be89-118">사용자에게 이 솔루션을 제공하기 위해 네트워크 인프라를 변경하거나 VPN을 요구할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-118">You don't need to change the network infrastructure or require VPN to provide this solution for your users.</span></span>

## <a name="why-is-application-proxy-a-better-solution"></a><span data-ttu-id="5be89-119">응용 프로그램 프록시가 더 나은 솔루션인 이유</span><span class="sxs-lookup"><span data-stu-id="5be89-119">Why is Application Proxy a better solution?</span></span>
<span data-ttu-id="5be89-120">Azure AD 응용 프로그램 프록시는 모든 온-프레미스 응용 프로그램에 대해 단순하고 보안되고 비용 효율적인 원격 액세스 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-120">Azure AD Application Proxy provides a simple, secure, and cost-effective remote access solution to all your on-premises applications.</span></span>

<span data-ttu-id="5be89-121">Azure AD 응용 프로그램 프록시는:</span><span class="sxs-lookup"><span data-stu-id="5be89-121">Azure AD Application Proxy is:</span></span>

* <span data-ttu-id="5be89-122">**간단**</span><span class="sxs-lookup"><span data-stu-id="5be89-122">**Simple**</span></span>
   * <span data-ttu-id="5be89-123">응용 프로그램 프록시를 사용하도록 응용 프로그램을 변경하거나 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-123">You don't need to change or update your applications to work with Application Proxy.</span></span> 
   * <span data-ttu-id="5be89-124">사용자는 일관된 인증 환경을 제공 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-124">Your users get a consistent authentication experience.</span></span> <span data-ttu-id="5be89-125">MyApps 포털을 사용하여 클라우드 및 앱 온-프레미스의 SaaS 앱에 Single Sign-On을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-125">They can use the MyApps portal to get single sign-on to both SaaS apps in the cloud and your apps on-premises.</span></span> 
* <span data-ttu-id="5be89-126">**보안**</span><span class="sxs-lookup"><span data-stu-id="5be89-126">**Secure**</span></span>
   * <span data-ttu-id="5be89-127">Azure AD 응용 프로그램 프록시를 사용하여 앱을 게시하면 Azure의 다양한 권한 부여 제어 및 보안 분석을 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-127">When you publish your apps using Azure AD Application Proxy, you can take advantage of the rich authorization controls and security analytics in Azure.</span></span> <span data-ttu-id="5be89-128">조건부 액세스 및 2단계 인증과 같은 클라우드 규모 보안 및 Azure 보안 기능을 제공 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-128">You get cloud-scale security and Azure security features like conditional access and two-step verification.</span></span>
   * <span data-ttu-id="5be89-129">사용자에게 원격 액세스를 제공하도록 방화벽을 통해 모든 인바운드 연결을 열 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-129">You don't have to open any inbound connections through your firewall to give your users remote access.</span></span> 
* <span data-ttu-id="5be89-130">**비용 효율성**</span><span class="sxs-lookup"><span data-stu-id="5be89-130">**Cost-effective**</span></span>
   * <span data-ttu-id="5be89-131">응용 프로그램 프록시는 클라우드에서 작업하므로 시간과 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-131">Application Proxy works in the cloud, so you can save time and money.</span></span> <span data-ttu-id="5be89-132">온-프레미스 솔루션을 사용하려면 일반적으로 DMZ, 에지 서버 또는 기타 복잡한 인프라를 설정하고 유지 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-132">On-premises solutions typically require you to set up and maintain DMZs, edge servers, or other complex infrastructures.</span></span>  

## <a name="what-kind-of-applications-work-with-application-proxy"></a><span data-ttu-id="5be89-133">어떤 종류의 응용 프로그램이 응용 프로그램 프록시에서 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="5be89-133">What kind of applications work with Application Proxy?</span></span>
<span data-ttu-id="5be89-134">Azure AD 응용 프로그램 프록시를 사용하면 다양한 유형의 내부 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-134">With Azure AD Application Proxy you can access different types of internal applications:</span></span>

* <span data-ttu-id="5be89-135">인증을 위해 [Windows 통합 인증](active-directory-application-proxy-sso-using-kcd.md)을 사용하는 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5be89-135">Web applications that use [Integrated Windows Authentication](active-directory-application-proxy-sso-using-kcd.md) for authentication</span></span>  
* <span data-ttu-id="5be89-136">폼 기반 또는 [헤더 기반](application-proxy-ping-access.md) 액세스를 사용하는 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5be89-136">Web applications that use form-based or [header-based](application-proxy-ping-access.md) access</span></span>  
* <span data-ttu-id="5be89-137">여러 장치에서 다양한 응용 프로그램을 표시하려는 웹 API</span><span class="sxs-lookup"><span data-stu-id="5be89-137">Web APIs that you want to expose to rich applications on different devices</span></span>  
* <span data-ttu-id="5be89-138">[원격 데스크톱 게이트웨이](application-proxy-publish-remote-desktop.md) 뒤에서 호스트되는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5be89-138">Applications hosted behind a [Remote Desktop Gateway](application-proxy-publish-remote-desktop.md)</span></span>  
* <span data-ttu-id="5be89-139">ADAL(Active Directory 인증 라이브러리)과 통합되는 리치 클라이언트 앱</span><span class="sxs-lookup"><span data-stu-id="5be89-139">Rich client apps that are integrated with the Active Directory Authentication Library (ADAL)</span></span>

## <a name="how-does-application-proxy-work"></a><span data-ttu-id="5be89-140">응용 프로그램 프록시는 어떻게 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="5be89-140">How does Application Proxy work?</span></span>
<span data-ttu-id="5be89-141">응용 프로그램 프록시가 작동하도록 구성해야 하는 두 가지 구성 요소는 커넥터 및 외부 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-141">There are two components that you need to configure to make Application Proxy work: a connector and an external endpoint.</span></span> 

<span data-ttu-id="5be89-142">커넥터는 네트워크 내부의 Windows Server에 상주하는 간단한 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-142">The connector is a lightweight agent that sits on a Windows Server inside your network.</span></span> <span data-ttu-id="5be89-143">커넥터는 클라우드의 응용 프로그램 프록시 서비스에서 응용 프로그램 온-프레미스로 트래픽 흐름을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-143">The connector facilitates the traffic flow from the Application Proxy service in the cloud to your application on-premises.</span></span> <span data-ttu-id="5be89-144">아웃바운드 연결만 사용하므로 인바운드 포트를 열거나 DMZ에 항목을 저장할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-144">It only uses outbound connections, so you don't have to open any inbound ports or put anything in the DMZ.</span></span> <span data-ttu-id="5be89-145">커넥터는 상태를 저장하지 않으며 필요에 따라 클라우드에서 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-145">The connectors are stateless and pull information from the cloud as necessary.</span></span> <span data-ttu-id="5be89-146">커넥터에 대한 정보 및 부하 분산 및 인증하는 방법은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5be89-146">For more information about connectors, like how they load-balance and authenticate, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span> 

<span data-ttu-id="5be89-147">외부 끝점은 사용자가 네트워크 외부에서 응용 프로그램에 도달하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-147">The external endpoint is how your users reach your applications while outside of your network.</span></span> <span data-ttu-id="5be89-148">결정하는 외부 URL로 직접 이동하거나 MyApps 포털을 통해 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-148">They can either go directly to an external URL that you determine, or they can access the application through the MyApps portal.</span></span> <span data-ttu-id="5be89-149">사용자가 이러한 끝점 중 하나로 이동하면 Azure AD에서 인증한 다음 커넥터를 통해 온-프레미스 응용 프로그램에 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-149">When users go to one of these endpoints, they authenticate in Azure AD and then are routed through the connector to the on-premises application.</span></span>

 ![Azure Ad 응용 프로그램 프록시 다이어그램](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. <span data-ttu-id="5be89-151">사용자는 응용 프로그램 프록시 서비스를 통해 응용 프로그램에 액세스하고 인증을 위해 Azure AD 로그인 페이지로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-151">The user accesses the application through the Application Proxy service and is directed to the Azure AD sign-in page to authenticate.</span></span>
2. <span data-ttu-id="5be89-152">성공적인 로그인 후에 토큰을 생성하고 클라이언트 장치에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-152">After a successful sign-in, a token is generated and sent to the client device.</span></span>
3. <span data-ttu-id="5be89-153">클라이언트는 토큰에서 UPN(사용자 주체 이름) 및 SPN(보안 주체 이름)을 검색한 다음 응용 프로그램 프록시 커넥터에 요청을 전달하는 응용 프로그램 프록시 서비스에 토큰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-153">The client sends the token to the Application Proxy service, which retrieves the user principal name (UPN) and security principal name (SPN) from the token, then directs the request to the Application Proxy connector.</span></span>
4. <span data-ttu-id="5be89-154">Single Sign-On을 구성한 경우 커넥터는 사용자를 대신하는 데 필요한 모든 추가 인증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-154">If you have configured single sign-on, the connector performs any additional authentication required on behalf of the user.</span></span>
5. <span data-ttu-id="5be89-155">커넥터는 온-프레미스 응용 프로그램에 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-155">The connector sends the request to the on-premises application.</span></span>  
6. <span data-ttu-id="5be89-156">응답은 응용 프로그램 프록시 서비스 및 커넥터를 통해 사용자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-156">The response is sent through Application Proxy service and connector to the user.</span></span>

### <a name="single-sign-on"></a><span data-ttu-id="5be89-157">SSO(Single sign-on)</span><span class="sxs-lookup"><span data-stu-id="5be89-157">Single sign-on</span></span>
<span data-ttu-id="5be89-158">Azure AD 응용 프로그램 프록시는 Windows 통합 인증(IWA) 또는 클레임 인식 응용 프로그램을 사용하는 응용 프로그램에 SSO(Single Sign-On)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-158">Azure AD Application Proxy provides single sign-on (SSO) to applications that use Integrated Windows Authentication (IWA), or claims-aware applications.</span></span> <span data-ttu-id="5be89-159">응용 프로그램에서 IWA를 사용하는 경우 응용 프로그램 프록시는 SSO를 제공하는 Kerberos 제한 위임을 사용하여 사용자를 가장합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-159">If your application uses IWA, Application Proxy impersonates the user using Kerberos Constrained Delegation to provide SSO.</span></span> <span data-ttu-id="5be89-160">Azure Active Directory를 신뢰하는 클레임 인식 응용 프로그램이 있는 경우에는 사용자가 이미 Azure AD에 의해 인증되었으므로 SSO가 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-160">If you have a claims-aware application that trusts Azure Active Directory, SSO works because the user was already authenticated by Azure AD.</span></span>

<span data-ttu-id="5be89-161">Kerberos에 대한 자세한 내용은 [KCD(Kerberos Constrained Delegation)에 대해 확인하려는 모든 정보](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5be89-161">For more information about Kerberos, see [All you want to know about Kerberos Constrained Delegation (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).</span></span>

### <a name="managing-apps"></a><span data-ttu-id="5be89-162">앱 관리</span><span class="sxs-lookup"><span data-stu-id="5be89-162">Managing apps</span></span>
<span data-ttu-id="5be89-163">응용 프로그램 프록시를 사용하여 앱이 게시되면 Azure Portal에서 다른 엔터프라이즈 앱처럼 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-163">One your app is published with Application Proxy, you can manage it like any other enterprise app in the Azure portal.</span></span> <span data-ttu-id="5be89-164">조건부 액세스 및 2단계 인증과 같은 Azure Active Directory 보안 기능을 사용하고, 사용자 권한을 제어하고, 앱에 대한 브랜딩을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-164">You can use Azure Active Directory security features like conditional access and two-step verification, control user permissions, and customize the branding for your app.</span></span> 

## <a name="get-started"></a><span data-ttu-id="5be89-165">시작</span><span class="sxs-lookup"><span data-stu-id="5be89-165">Get started</span></span>

<span data-ttu-id="5be89-166">응용 프로그램 프록시를 구성하기 전에 지원되는 [Azure Active Directory 버전](https://azure.microsoft.com/pricing/details/active-directory/) 및 전역 관리자 권한이 있는 Azure AD 디렉터리가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-166">Before you configure Application Proxy, make sure you have a supported [Azure Active Directory edition](https://azure.microsoft.com/pricing/details/active-directory/) and an Azure AD directory for which you are a global administrator.</span></span>

<span data-ttu-id="5be89-167">두 단계에서 응용 프로그램 프록시 시작:</span><span class="sxs-lookup"><span data-stu-id="5be89-167">Get started with Application Proxy in two steps:</span></span>

1. <span data-ttu-id="5be89-168">[응용 프로그램 프록시를 사용하도록 설정하고 커넥터 구성](active-directory-application-proxy-enable.md)</span><span class="sxs-lookup"><span data-stu-id="5be89-168">[Enable Application Proxy and configure the connector](active-directory-application-proxy-enable.md).</span></span>    
2. <span data-ttu-id="5be89-169">[응용 프로그램 게시](active-directory-application-proxy-publish.md) - 쉽고 빠른 마법사를 사용하여 온-프레미스 앱을 게시하고 원격으로 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-169">[Publish applications](active-directory-application-proxy-publish.md) - use the quick and easy wizard to get your on-premises apps published and accessible remotely.</span></span>

## <a name="whats-next"></a><span data-ttu-id="5be89-170">다음 작업</span><span class="sxs-lookup"><span data-stu-id="5be89-170">What's next?</span></span>
<span data-ttu-id="5be89-171">첫 번째 앱을 게시하면 응용 프로그램 프록시를 사용하여 수행할 수 있는 작업은 많습니다.</span><span class="sxs-lookup"><span data-stu-id="5be89-171">Once you publish your first app, there's a lot more you can do with Application Proxy:</span></span>

* [<span data-ttu-id="5be89-172">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="5be89-172">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="5be89-173">고유한 도메인 이름을 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="5be89-173">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="5be89-174">Azure AD 응용 프로그램 프록시 커넥터에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="5be89-174">Learn about Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
* [<span data-ttu-id="5be89-175">기존 온-프레미스 프록시 서버 작업</span><span class="sxs-lookup"><span data-stu-id="5be89-175">Working with existing on-premises Proxy servers</span></span>](application-proxy-working-with-proxy-servers.md) 
* [<span data-ttu-id="5be89-176">사용자 지정 홈페이지 설정</span><span class="sxs-lookup"><span data-stu-id="5be89-176">Set a custom home page</span></span>](application-proxy-office365-app-launcher.md)

<span data-ttu-id="5be89-177">최신 뉴스 및 업데이트는 [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="5be89-177">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>

