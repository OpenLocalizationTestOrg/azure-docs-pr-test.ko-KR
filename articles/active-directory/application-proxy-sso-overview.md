---
title: "Azure AD 응용 프로그램 프록시용 SSO 관리 | Microsoft Docs"
description: "응용 프로그램 프록시의 Single Sign-On 기본 사항 알아보기"
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
ms.openlocfilehash: 1deb3d91049d45fe26791783e13bd23e0a7d9f95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="dd2e7-103">Azure AD 응용 프로그램 프록시에서 Single Sign-On을 제공하는 방법</span><span class="sxs-lookup"><span data-stu-id="dd2e7-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="dd2e7-104">Single Sign-On은 Azure AD 응용 프로그램 프록시의 핵심 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="dd2e7-105">사용자가 클라우드에서 Azure Active Directory에만 로그인하면 되기 때문에 최상의 사용자 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-105">It provides the best user experience because your users only have to sign in to Azure Active Directory in the cloud.</span></span> <span data-ttu-id="dd2e7-106">사용자가 Azure Active Directory에 인증하면 응용 프로그램 프록시 커넥터에서 온-프레미스 응용 프로그램에 대한 인증을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-106">Once they authenticate to Azure Active Directory, the Application Proxy connector handles the authentication to the on-premises application.</span></span> <span data-ttu-id="dd2e7-107">백 엔드 응용 프로그램은 응용 프로그램 프록시를 통한 원격 사용자 로그인과 도메인에 가입된 장치의 정상적인 사용 간 차이점을 구별할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-107">The backend application can't tell the difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="dd2e7-108">응용 프로그램 Single Sign-On에 Azure Active Directory를 사용하려면 사전 인증 방법으로 **Azure Active Directory**를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-108">To use Azure Active Directory for single sign-on to your applications, you need to select **Azure Active Directory** as the pre-authentication method.</span></span> <span data-ttu-id="dd2e7-109">**통과**를 선택하면 사용자가 Azure Active Directory에 전혀 인증되지 않고 바로 응용 프로그램으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-109">If you select **Passthrough** then your users don't authenticate to Azure Active Directory at all, but are directed straight to the application.</span></span> <span data-ttu-id="dd2e7-110">응용 프로그램을 처음으로 게시할 때 이 설정을 구성할 수도 있고, Azure Portal에서 응용 프로그램으로 이동하여 응용 프로그램 프록시 설정을 편집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-110">You can configure this setting when you first publish an application, or navigate to your application in the Azure portal and edit the Application Proxy settings.</span></span> 

<span data-ttu-id="dd2e7-111">Single Sign-On 옵션을 보려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-111">To see your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="dd2e7-112">[Azure portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-112">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dd2e7-113">**Azure Active Directory** > **Enterprise 응용 프로그램** > **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-113">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="dd2e7-114">Single Sign-On 옵션을 관리하려는 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-114">Select the app whose single sign-on options you want to manage.</span></span>
4. <span data-ttu-id="dd2e7-115">**Single Sign-On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-115">Select **Single sign-on**.</span></span>

   ![SSO 드롭다운 메뉴](./media/application-proxy-sso-overview/single-sign-on-mode.png)

<span data-ttu-id="dd2e7-117">드롭다운 메뉴에는 응용 프로그램 Single Sign-On에 대한 5가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-117">The dropdown menu shows five options for single sign-on to your application:</span></span>

* <span data-ttu-id="dd2e7-118">Azure AD Single Sign-On 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="dd2e7-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="dd2e7-119">암호 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="dd2e7-119">Password-based sign-on</span></span>
* <span data-ttu-id="dd2e7-120">연결된 로그온</span><span class="sxs-lookup"><span data-stu-id="dd2e7-120">Linked sign-on</span></span>
* <span data-ttu-id="dd2e7-121">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="dd2e7-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="dd2e7-122">헤더 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="dd2e7-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="dd2e7-123">Azure AD Single Sign-On 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="dd2e7-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="dd2e7-124">응용 프로그램에 Azure Active Directory Single Sign-On 통합을 사용하지 않으려면 **Azure AD Single Sign-On 사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-124">If you don't want to use Azure Active Directory integration for single sign-on to your application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="dd2e7-125">이 옵션을 선택하면 사용자가 두 번 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="dd2e7-126">첫 번째로, Azure Active Directory에 인증한 후 응용 프로그램 자체에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-126">First, they authenticate to Azure Active Directory and then sign in to the application itself.</span></span> 

<span data-ttu-id="dd2e7-127">이 옵션은 사용자가 온-프레미스 응용 프로그램에 인증하지 않아도 되지만 Azure Active Directory를 원격 액세스의 보안 레이어로 추가하려는 경우에 적합한 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-127">This option is a good choice if your on-premises application doesn't require users to authenticate, but you want to add Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="dd2e7-128">암호 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="dd2e7-128">Password-based sign-on</span></span>

<span data-ttu-id="dd2e7-129">Azure Active Directory를 온-프레미스 응용 프로그램의 암호 자격 증명으로 사용하려는 경우 **암호 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-129">If you want to use Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="dd2e7-130">이 옵션은 응용 프로그램에서 액세스 토큰 또는 헤더 대신 사용자 이름/암호 조합을 사용하여 인증하는 경우에 적합한 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="dd2e7-131">암호 기반 로그온을 사용하면 사용자가 응용 프로그램에 처음으로 액세스할 때 응용 프로그램에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-131">With password-based sign-on, your users need to sign in to the application the first time they access it.</span></span> <span data-ttu-id="dd2e7-132">그 후에는 Azure Active Directory가 사용자를 대신하여 사용자 이름 및 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-132">After that, Azure Active Directory supplies the username and password on behalf of the user.</span></span> 

<span data-ttu-id="dd2e7-133">암호 기반 로그온 설정에 대한 내용은 [응용 프로그램 프록시를 사용하여 Single Sign-On에 대한 암호 자격 증명 모음 설정](application-proxy-sso-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-sso-azure-portal.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="dd2e7-134">연결된 로그온</span><span class="sxs-lookup"><span data-stu-id="dd2e7-134">Linked sign-on</span></span>

<span data-ttu-id="dd2e7-135">온-프레미스 ID에 대한 Single Sign-On 솔루션이 이미 설치된 경우 **연결된 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="dd2e7-136">이 옵션을 사용하면 Azure Active Directory가 기존 SSO 솔루션을 활용하지만, 사용자에게 응용 프로그램에 대한 원격 액세스를 계속 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-136">This option enables Azure Active Directory to leverage existing SSO solutions, but still gives your users remote access to the application.</span></span> 

<span data-ttu-id="dd2e7-137">연결된 로그온(공식적으로 기존 Single Sign-On으로 알려짐)에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="dd2e7-138">Windows 통합 인증</span><span class="sxs-lookup"><span data-stu-id="dd2e7-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="dd2e7-139">온-프레미스 응용 프로그램에서 IWA(Windows 통합 인증)를 사용하거나 Single Sign-On에 KCD(Kerberos 제한된 위임)를 사용하려는 경우 **Windows 통합 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want to use Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="dd2e7-140">이 옵션을 선택하면 사용자가 Azure Active Directory에만 인증하면 됩니다. 그러면 응용 프로그램 프록시 커넥터가 사용자를 가장하여 Kerberos 토큰을 가져오고 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-140">With this option, your users only need to authenticate to Azure Active Directory, and then the Application Proxy connector impersonates the user to get a Kerberos token and sign in to the application.</span></span> 

<span data-ttu-id="dd2e7-141">Windows 통합 인증 설정에 대한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 Kerberos 제한된 위임](active-directory-application-proxy-sso-using-kcd.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="dd2e7-142">헤더 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="dd2e7-142">Header-based sign-on</span></span> 

<span data-ttu-id="dd2e7-143">응용 프로그램에서 인증에 헤더를 사용하는 경우 **헤더 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="dd2e7-144">이 옵션을 선택하면 사용자가 Azure Active Directory에만 인증하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-144">With this option, your users only need to authentication the Azure Active Directory.</span></span> <span data-ttu-id="dd2e7-145">Microsoft는 PingAccess라고 하는 타사 인증 서비스를 사용하는데, 이 서비스는 Azure Active Directory 액세스 토큰을 응용 프로그램의 헤더 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-145">Microsoft partners with a third-party authentication service called PingAccess, which translated the Azure Active Directory access token into a header format for the application.</span></span> 

<span data-ttu-id="dd2e7-146">헤더 기반 인증 설정에 대한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 헤더 기반 인증](application-proxy-ping-access.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd2e7-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd2e7-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd2e7-147">Next steps</span></span>

- [<span data-ttu-id="dd2e7-148">응용 프로그램 프록시를 사용하여 Single Sign-On에 대한 암호 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="dd2e7-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-sso-azure-portal.md)
- [<span data-ttu-id="dd2e7-149">응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 Kerberos 제한된 위임</span><span class="sxs-lookup"><span data-stu-id="dd2e7-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="dd2e7-150">응용 프로그램 프록시를 사용하는 Single Sign-On에 대한 헤더 기반 인증</span><span class="sxs-lookup"><span data-stu-id="dd2e7-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-ping-access.md) 
