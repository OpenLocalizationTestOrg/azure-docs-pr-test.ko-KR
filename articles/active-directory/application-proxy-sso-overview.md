---
title: "Azure AD 응용 프로그램 프록시에 대 한 SSO aaaManage | Microsoft Docs"
description: "Single sign-on의 응용 프로그램 프록시 hello 기본 사항에 알아보기"
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
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="86ee2-103">Azure AD 응용 프로그램 프록시에서 Single Sign-On을 제공하는 방법</span><span class="sxs-lookup"><span data-stu-id="86ee2-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="86ee2-104">Single Sign-On은 Azure AD 응용 프로그램 프록시의 핵심 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="86ee2-105">사용자가 하나만 있으므로 toosign tooAzure hello 클라우드에 Active Directory에에서 hello 최상의 사용자 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-105">It provides hello best user experience because your users only have toosign in tooAzure Active Directory in hello cloud.</span></span> <span data-ttu-id="86ee2-106">TooAzure Active Directory 인증 되 면 hello 응용 프로그램 프록시 커넥터는 온-프레미스 응용 프로그램을 toohello hello 인증을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-106">Once they authenticate tooAzure Active Directory, hello Application Proxy connector handles hello authentication toohello on-premises application.</span></span> <span data-ttu-id="86ee2-107">hello 백 엔드 응용 프로그램 도메인에 가입 된 장치에 정상적인 사용 및 응용 프로그램 프록시를 통해 로그인 하는 원격 사용자의 hello 차이 구별할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-107">hello backend application can't tell hello difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="86ee2-108">single sign on tooyour 응용 프로그램에 대 한 Azure Active Directory를 toouse, 해야 tooselect **Azure Active Directory** hello 사전 인증 방법으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-108">toouse Azure Active Directory for single sign-on tooyour applications, you need tooselect **Azure Active Directory** as hello pre-authentication method.</span></span> <span data-ttu-id="86ee2-109">선택 하는 경우 **통과** 사용자에 게 전혀 tooAzure Active Directory를 인증 하지 않고 되지만 직선 toohello 방향이 지정 된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-109">If you select **Passthrough** then your users don't authenticate tooAzure Active Directory at all, but are directed straight toohello application.</span></span> <span data-ttu-id="86ee2-110">먼저 응용 프로그램을 게시 또는 hello Azure 포털에서에서 tooyour 응용 프로그램을 이동 하 고 hello 응용 프로그램 프록시 설정을 편집이 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-110">You can configure this setting when you first publish an application, or navigate tooyour application in hello Azure portal and edit hello Application Proxy settings.</span></span> 

<span data-ttu-id="86ee2-111">toosee single sign on 옵션을 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-111">toosee your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="86ee2-112">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-112">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="86ee2-113">너무 이동**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-113">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="86ee2-114">해당에서 single sign-on 옵션을 선택 hello 앱 toomanage를 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-114">Select hello app whose single sign-on options you want toomanage.</span></span>
4. <span data-ttu-id="86ee2-115">**Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-115">Select **Single sign-on**.</span></span>

   ![SSO 드롭다운 메뉴](./media/application-proxy-sso-overview/single-sign-on-mode.png)

<span data-ttu-id="86ee2-117">hello 드롭다운 메뉴에는 single sign on tooyour 응용 프로그램에 대 한 다섯 가지 옵션이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-117">hello dropdown menu shows five options for single sign-on tooyour application:</span></span>

* <span data-ttu-id="86ee2-118">Azure AD Single Sign-On 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="86ee2-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="86ee2-119">암호 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="86ee2-119">Password-based sign-on</span></span>
* <span data-ttu-id="86ee2-120">연결된 로그온</span><span class="sxs-lookup"><span data-stu-id="86ee2-120">Linked sign-on</span></span>
* <span data-ttu-id="86ee2-121">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="86ee2-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="86ee2-122">헤더 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="86ee2-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="86ee2-123">Azure AD Single Sign-On 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="86ee2-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="86ee2-124">Single sign on tooyour 응용 프로그램에 대 한 toouse Azure Active Directory 통합을 사용 하지 않으려는 경우 선택 **Azure AD에서 single sign-on 사용 하지 않도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-124">If you don't want toouse Azure Active Directory integration for single sign-on tooyour application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="86ee2-125">이 옵션을 선택하면 사용자가 두 번 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="86ee2-126">첫째, tooAzure Active Directory 인증 하 고 toohello 응용 프로그램 자체에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-126">First, they authenticate tooAzure Active Directory and then sign in toohello application itself.</span></span> 

<span data-ttu-id="86ee2-127">이 옵션은 온-프레미스 응용 프로그램 사용자 tooauthenticate 필요 하지 않습니다 있지만 원격 액세스에 대 한 보안 계층으로 tooadd Azure Active Directory를 수행 하는 경우에 적합 한 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-127">This option is a good choice if your on-premises application doesn't require users tooauthenticate, but you want tooadd Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="86ee2-128">암호 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="86ee2-128">Password-based sign-on</span></span>

<span data-ttu-id="86ee2-129">온-프레미스 응용 프로그램에 대 한 Azure Active Directory toouse 암호 자격 증명 모음으로 하려는 경우 선택 **암호 기반 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-129">If you want toouse Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="86ee2-130">이 옵션은 응용 프로그램에서 액세스 토큰 또는 헤더 대신 사용자 이름/암호 조합을 사용하여 인증하는 경우에 적합한 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="86ee2-131">암호 기반 로그온 사용자에 게 필요 toosign toohello 응용 프로그램 hello에 처음으로 액세스 하는 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-131">With password-based sign-on, your users need toosign in toohello application hello first time they access it.</span></span> <span data-ttu-id="86ee2-132">그 후 Azure Active Directory hello 사용자를 대신 하 여 hello 사용자 이름 및 암호 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-132">After that, Azure Active Directory supplies hello username and password on behalf of hello user.</span></span> 

<span data-ttu-id="86ee2-133">암호 기반 로그온 설정에 대한 내용은 [응용 프로그램 프록시를 사용하여 Single Sign-On에 대한 암호 자격 증명 모음 설정](application-proxy-sso-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86ee2-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-sso-azure-portal.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="86ee2-134">연결된 로그온</span><span class="sxs-lookup"><span data-stu-id="86ee2-134">Linked sign-on</span></span>

<span data-ttu-id="86ee2-135">온-프레미스 ID에 대한 Single Sign-On 솔루션이 이미 설치된 경우 **연결된 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="86ee2-136">이 옵션을 통해 Azure Active Directory tooleverage 기존 SSO 솔루션 하지만 원격 액세스 toohello 응용 프로그램 사용자가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-136">This option enables Azure Active Directory tooleverage existing SSO solutions, but still gives your users remote access toohello application.</span></span> 

<span data-ttu-id="86ee2-137">연결된 로그온(공식적으로 기존 Single Sign-On으로 알려짐)에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86ee2-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="86ee2-138">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="86ee2-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="86ee2-139">온-프레미스 응용 프로그램에서 통합 Windows Authentication(IWA) 사용 또는 single sign on toouse KCD Kerberos 제한 위임 ()를 사용 하려는 경우 선택 **Windows 통합 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want toouse Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="86ee2-140">이 옵션을 사용 사용자 권한만 tooauthenticate tooAzure Active Directory 및 그런 다음 응용 프로그램 프록시 커넥터 hello 가장 hello 사용자 tooget Kerberos 토큰 및 toohello 응용 프로그램에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-140">With this option, your users only need tooauthenticate tooAzure Active Directory, and then hello Application Proxy connector impersonates hello user tooget a Kerberos token and sign in toohello application.</span></span> 

<span data-ttu-id="86ee2-141">Windows 통합 인증 설정에 대한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 Kerberos 제한된 위임](active-directory-application-proxy-sso-using-kcd.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86ee2-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="86ee2-142">헤더 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="86ee2-142">Header-based sign-on</span></span> 

<span data-ttu-id="86ee2-143">응용 프로그램에서 인증에 헤더를 사용하는 경우 **헤더 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="86ee2-144">이 옵션을 사용 하면 사용자는 Azure Active Directory tooauthentication hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-144">With this option, your users only need tooauthentication hello Azure Active Directory.</span></span> <span data-ttu-id="86ee2-145">타사 인증 서비스와 Microsoft 파트너 PingAccess hello 응용 프로그램에 대 한 헤더 형식을으로 hello Azure Active Directory 액세스 토큰을 변환 하는 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86ee2-145">Microsoft partners with a third-party authentication service called PingAccess, which translated hello Azure Active Directory access token into a header format for hello application.</span></span> 

<span data-ttu-id="86ee2-146">헤더 기반 인증 설정에 대한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 헤더 기반 인증](application-proxy-ping-access.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86ee2-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86ee2-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86ee2-147">Next steps</span></span>

- [<span data-ttu-id="86ee2-148">응용 프로그램 프록시를 사용하여 Single Sign-On에 대한 암호 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="86ee2-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-sso-azure-portal.md)
- [<span data-ttu-id="86ee2-149">응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 Kerberos 제한된 위임</span><span class="sxs-lookup"><span data-stu-id="86ee2-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="86ee2-150">응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 헤더 기반 인증</span><span class="sxs-lookup"><span data-stu-id="86ee2-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-ping-access.md) 
