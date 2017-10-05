---
title: "사용할 Single Sign-On 방법을 결정하는 방법 | Microsoft Docs"
description: "Azure AD에서 지원되는 Single Sign-On 모드 및 관심 있는 응용 프로그램에 대해 사용할 모드를 선택하는 방법을 이해합니다."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 80f4a965920fec9cb578c1bee235c7857f37431e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-determine-what-single-sign-on-method-to-use"></a><span data-ttu-id="afd62-103">사용할 Single Sign-On 방법을 결정하는 방법</span><span class="sxs-lookup"><span data-stu-id="afd62-103">How to determine what single-sign on method to use</span></span>

<span data-ttu-id="afd62-104">이 문서에서는 Azure AD에서 지원되는 Single Sign-On 모드 및 관심 있는 응용 프로그램에 대해 사용할 모드를 선택하는 방법을 이해하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-104">This article help you to understand the single sign-on modes supported by Azure AD and how to pick which one to choose for the application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="afd62-105">특정 응용 프로그램 형식에서 지원되는 Single Sign-On 및 프로비전 모드</span><span class="sxs-lookup"><span data-stu-id="afd62-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="afd62-106">다음 표는 위의 각 응용 프로그램 형식에서 지원하는 서로 다른 Single Sign-On 및 프로비전 모드를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-106">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="afd62-107">이 표를 사용하여 특정 목표를 지원하기 위해 추가해야 하는 응용 프로그램을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-107">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![앱 형식 표](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="afd62-109">Single Sign-On 모드를 선택하는 방법</span><span class="sxs-lookup"><span data-stu-id="afd62-109">How to choose a single sign-on mode</span></span>

<span data-ttu-id="afd62-110">Azure AD 응용 프로그램에 대해 지원되는 **Single Sign-On** 모드는 아래에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-110">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="afd62-111">**Azure AD Single Sign-On 사용 안 함** – 이 응용 프로그램을 Single Sign-On을 사용하여 Azure AD와 통합할 준비가 되지 않았거나 단순히 테스트하는 경우 Azure AD Single Sign-On 사용 안 함 **Single Sign-On 모드** 선택</span><span class="sxs-lookup"><span data-stu-id="afd62-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="afd62-112">**연결된 로그온** - 기존 Single Sign-On 솔루션에 연결된 응용 프로그램이 있거나 [응용 프로그램 액세스 패널](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) 또는 [Office 365 응용 프로그램 시작 관리자](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)에서 사용자에게 간단한 링크를 배포하려는 경우 [연결된 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **Single Sign-On 모드** 선택</span><span class="sxs-lookup"><span data-stu-id="afd62-112">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="afd62-113">**암호 기반 로그온** - 응용 프로그램이 HTML 사용자 이름 및 암호 필드를 렌더링하고 해당 사용자 이름 및 암호가 나중에 응용 프로그램에 재생되도록 안전하게 저장하려는 경우 [암호 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **Single Sign-On 모드** 선택</span><span class="sxs-lookup"><span data-stu-id="afd62-113">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="afd62-114">**SAML 기반 로그온** - 응용 프로그램이 SAML 또는 OpenID Connect 프로토콜을 지원하거나 사용자를 SAML 클레임에서 정의하는 규칙에 따라 특정 응용 프로그램 역할에 매핑할 수 있게 되기를 원하는 경우 [SAML 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) Single Sign-On 모드 선택 *(**참고:** 응용 프로그램 프록시가 응용 프로그램에 대해 구성되어 있으면 이 옵션을 사용할 수 없음)*</span><span class="sxs-lookup"><span data-stu-id="afd62-114">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *(**Note:** this option is not available when the application proxy is configured for an application)*</span></span>

-   <span data-ttu-id="afd62-115">**헤더 기반 로그온** – Single Sign-On을 수행하려는 HTTP 헤더 기반 인증을 지원하는 PingAccess를 사용하는 응용 프로그램이 있는 경우 이 [헤더 기반 로그온](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) Single Sign-On 모드 선택 *(**참고:** 응용 프로그램 프록시 및 PingAccess가 응용 프로그램에 대해 구성되어 있을 때만 이 옵션을 사용할 수 있음)*</span><span class="sxs-lookup"><span data-stu-id="afd62-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy and PingAccess is configured for an application)*</span></span>

-   <span data-ttu-id="afd62-116">**Windows 통합 인증** - Single Sign-On을 수행하려는 온-프레미스 WIA 응용 프로그램을 노출하는 경우 [Windows 통합 인증](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) Single Sign-On 모드 선택 *(**참고:** 응용 프로그램 프록시가 응용 프로그램에 대해 구성되어 있을 때만 이 옵션을 사용할 수 있음)*</span><span class="sxs-lookup"><span data-stu-id="afd62-116">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy is configured for an application)*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="afd62-117">사용자 지정 개발된 응용 프로그램에 대한 Single Sign-On 모드</span><span class="sxs-lookup"><span data-stu-id="afd62-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="afd62-118">[사용자 지정 개발된 응용 프로그램](#_Custom-Developed_Applications) 환경을 통해 사용자 지정 개발한 응용 프로그램은 위에 나열되지 않은 추가 Single Sign-On 모드도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-118">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="afd62-119">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-119">These include:</span></span>

-   <span data-ttu-id="afd62-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="afd62-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="afd62-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="afd62-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="afd62-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="afd62-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="afd62-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="afd62-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="afd62-124">이러한 Single Sign-On 모드를 지원하는 사용자 지정 개발된 응용 프로그램을 만드는 방법에 대해 자세히 알아보려면 [Azure Active Directory 개발자 가이드](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd62-124">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="afd62-125">응용 프로그램의 Single Sign-On 모드를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="afd62-125">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="afd62-126">응용 프로그램의 **Single Sign-On** 모드를 설정하려면 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-126">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="afd62-127">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-127">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="afd62-128">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-128">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="afd62-129">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-129">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afd62-130">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-130">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="afd62-131">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-131">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="afd62-132">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-132">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afd62-133">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-133">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="afd62-134">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="afd62-134">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afd62-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="afd62-135">Next steps</span></span>
[<span data-ttu-id="afd62-136">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="afd62-136">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

