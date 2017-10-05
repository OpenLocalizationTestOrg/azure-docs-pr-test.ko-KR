---
title: "응용 프로그램을 추가할 때 사용할 응용 프로그램 형식을 선택하는 방법 | Microsoft Docs"
description: "Azure AD와 통합할 수 있는 지원되는 응용 프로그램의 형식 및 해당 관련 구성 옵션 이해"
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
ms.openlocfilehash: e0d41d1933531c2c633613bcbc1bbcbf075d6a69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-choose-which-application-type-to-use-when-adding-an-application"></a><span data-ttu-id="a8c0f-103">응용 프로그램을 추가할 때 사용할 응용 프로그램 형식을 선택하는 방법</span><span class="sxs-lookup"><span data-stu-id="a8c0f-103">How to choose which application type to use when adding an application</span></span>

<span data-ttu-id="a8c0f-104">이 문서는 Azure AD와 통합할 수 있는 네 가지 기본 응용 프로그램 형식을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="a8c0f-105">각 형식에 의해 지원되는 항목</span><span class="sxs-lookup"><span data-stu-id="a8c0f-105">What is supported by each of them</span></span>
* <span data-ttu-id="a8c0f-106">해당 응용 프로그램을 선택할 수도 있는 이유</span><span class="sxs-lookup"><span data-stu-id="a8c0f-106">Why you might choose which application</span></span>
* <span data-ttu-id="a8c0f-107">사용자가 **프로비전**되는 방법 또는 사용할 **Single Sign-On** 기술과 같은 해당 응용 프로그램의 핵심 속성을 구성하는 방법.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="a8c0f-108">Azure AD에서 지원되는 응용 프로그램 형식</span><span class="sxs-lookup"><span data-stu-id="a8c0f-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="a8c0f-109">Azure AD는 **엔터프라이즈 응용 프로그램** 아래에 있는 **추가** 기능을 사용하여 추가할 수 있는 네 가지 기본 응용 프로그램 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="a8c0f-110">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-110">These include:</span></span>

-   <span data-ttu-id="a8c0f-111">**Azure AD 갤러리 응용 프로그램** – Single Sign-On에 대해 Azure AD와 사전 통합된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="a8c0f-112">**응용 프로그램 프록시 응용 프로그램** – 외부로 보안 Single Sign-On을 제공하려는 온-프레미스 환경에서 실행 중인 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

-   <span data-ttu-id="a8c0f-113">**사용자 지정 개발된 응용 프로그램** – 조직에서 Azure AD 응용 프로그램 개발 플랫폼에서 개발하고자 하지만 아직 존재하지 않을 수 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="a8c0f-114">**비 갤러리 응용 프로그램** – 사용자의 응용 프로그램을 가져옵니다!</span><span class="sxs-lookup"><span data-stu-id="a8c0f-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="a8c0f-115">원하는 모든 웹 링크 또는 사용자 이름 및 암호 필드를 렌더링하는 모든 응용 프로그램은 SAML 또는 OpenID Connect 프로토콜을 지원하거나 Single Sign-On에 대해 Azure AD와 통합하려는 SCIM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-the-above-application-types"></a><span data-ttu-id="a8c0f-116">위의 모든 응용 프로그램 형식에서 지원되는 기능 및 특징</span><span class="sxs-lookup"><span data-stu-id="a8c0f-116">Features and capabilities supported by all the above application types</span></span>

<span data-ttu-id="a8c0f-117">다음 기능은 Azure AD에서 위의 4개의 응용 프로그램 형식 중 하나에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-117">The following features are supported by any of the above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="a8c0f-118">**빠른 시작** – [간단한 배포 단계](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)를 수행하여 신속하게 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="a8c0f-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="a8c0f-119">**일반 속성 관리** – 응용 프로그램에 [직접 딥 링크](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) 가져오기, 응용 프로그램의 [브랜딩 사용자 지정](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) 또는 모든 사용자에 대한 [응용 프로그램을 사용하지 않도록 설정](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="a8c0f-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="a8c0f-120">**사용자 및 그룹 관리** – 사용자 및 그룹을 응용 프로그램에 [할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) 또는 [제거](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) 및 경우에 따라 액세스를 가진 이러한 사용자 및 그룹에 특정 응용 프로그램 역할 할당</span><span class="sxs-lookup"><span data-stu-id="a8c0f-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="a8c0f-121">**셀프 서비스 응용 프로그램 액세스** - 사용자가 응용 프로그램을 직접 추가하거나 [셀프 서비스가 활성화된 그룹에 가입](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)하거나 경우에 따라 비즈니스 승인을 요구하여 응용 프로그램 액세스 패널에서 응용 프로그램에 대한 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)를 요청하도록 함</span><span class="sxs-lookup"><span data-stu-id="a8c0f-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span></span>

-   <span data-ttu-id="a8c0f-122">**로그인 로그** – [응용 프로그램에 대한 모든 로그인](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) 또는 모든 응용 프로그램 보기</span><span class="sxs-lookup"><span data-stu-id="a8c0f-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="a8c0f-123">**감사 로그** – [응용 프로그램 수정에 대한 자세한 감사 로그](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) 또는 모든 응용 프로그램 보기</span><span class="sxs-lookup"><span data-stu-id="a8c0f-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span></span>

-   <span data-ttu-id="a8c0f-124">**조건부 및 리스크 기반 액세스** - 사용자가 특정 응용 프로그램에 대한 로그인을 시도할 때 적용되는 강력한 [조건 기반 액세스 규칙](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) 설정</span><span class="sxs-lookup"><span data-stu-id="a8c0f-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span></span>

-   <span data-ttu-id="a8c0f-125">**사용 권한 보기** – 응용 프로그램이 단일 위치의 디렉터리에서 액세스를 갖는 [OAuth2 권한](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) 중 하나 보기</span><span class="sxs-lookup"><span data-stu-id="a8c0f-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="a8c0f-126">특정 응용 프로그램 형식에서 지원되는 Single Sign-On 및 프로비전 모드</span><span class="sxs-lookup"><span data-stu-id="a8c0f-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="a8c0f-127">다음 표는 위의 각 응용 프로그램 형식에서 지원하는 서로 다른 Single Sign-On 및 프로비전 모드를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-127">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="a8c0f-128">이 테이블을 사용하여 특정 목표를 지원하기 위해 추가해야 하는 응용 프로그램을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![앱 형식 테이블](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="a8c0f-130">Single Sign-On 모드를 선택하는 방법</span><span class="sxs-lookup"><span data-stu-id="a8c0f-130">How to choose a single sign-on mode</span></span>

<span data-ttu-id="a8c0f-131">Azure AD 응용 프로그램에 대해 지원되는 **Single Sign-On** 모드는 아래에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-131">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="a8c0f-132">**Azure AD Single Sign-On 사용 안 함** – 이 응용 프로그램을 Single Sign-On을 사용하여 Azure AD와 통합할 준비가 되지 않았거나 단순히 테스트하는 경우 Azure AD Single Sign-On 사용 안 함 **Single Sign-On 모드** 선택</span><span class="sxs-lookup"><span data-stu-id="a8c0f-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="a8c0f-133">**연결된 로그온** - 기존 Single Sign-On 솔루션에 연결된 응용 프로그램이 있거나 [응용 프로그램 액세스 패널](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) 또는 [Office 365 응용 프로그램 시작 관리자](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)에서 사용자에게 간단한 링크를 배포하려는 경우 [연결된 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **Single Sign-On 모드** 선택</span><span class="sxs-lookup"><span data-stu-id="a8c0f-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="a8c0f-134">**암호 기반 로그온** - 응용 프로그램이 HTML 사용자 이름 및 암호 필드를 렌더링하고 해당 사용자 이름 및 암호가 나중에 응용 프로그램에 재생되도록 안전하게 저장하려는 경우 [암호 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **Single Sign-On 모드** 선택</span><span class="sxs-lookup"><span data-stu-id="a8c0f-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="a8c0f-135">**SAML 기반 로그온** - 응용 프로그램이 SAML 또는 OpenID Connect 프로토콜을 지원하거나 사용자를 SAML 클레임에서 정의하는 규칙에 따라 특정 응용 프로그램 역할에 매핑할 수 있게 되기를 원하는 경우 [SAML 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) Single Sign-On 모드 선택 *</span><span class="sxs-lookup"><span data-stu-id="a8c0f-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="a8c0f-136">응용 프로그램 프록시가 응용 프로그램에 대해 구성된 경우 이 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-136">This option is not available when the application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="a8c0f-137">**헤더 기반 로그온** – Single Sign-On을 수행하려는 HTTP 헤더 기반 인증을 지원하는 PingAccess를 사용하는 응용 프로그램이 있는 경우 이 [헤더 기반 로그온](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) Single Sign-On 모드 선택</span><span class="sxs-lookup"><span data-stu-id="a8c0f-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="a8c0f-138">응용 프로그램 프록시 및 PingAccess가 응용 프로그램에 대해 구성된 경우에만 이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-138">This option is only available when the application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="a8c0f-139">**Windows 통합 인증** - Single Sign-On을 수행하려는 온-프레미스 WIA 응용 프로그램을 노출하는 경우 [Windows 통합 인증](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) Single Sign-On 모드 선택</span><span class="sxs-lookup"><span data-stu-id="a8c0f-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="a8c0f-140">응용 프로그램 프록시가 응용 프로그램에 대해 구성된 경우에만 이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-140">This option is only available when the application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="a8c0f-141">사용자 지정 개발된 응용 프로그램에 대한 Single Sign-On 모드</span><span class="sxs-lookup"><span data-stu-id="a8c0f-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="a8c0f-142">[사용자 지정 개발된 응용 프로그램](#_Custom-Developed_Applications) 환경을 통해 사용자 지정 개발한 응용 프로그램은 위에 나열되지 않은 추가 Single Sign-On 모드도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="a8c0f-143">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-143">These include:</span></span>

-   <span data-ttu-id="a8c0f-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="a8c0f-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="a8c0f-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="a8c0f-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="a8c0f-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="a8c0f-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="a8c0f-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="a8c0f-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="a8c0f-148">이러한 Single Sign-On 모드를 지원하는 사용자 지정 개발된 응용 프로그램을 만드는 방법에 대해 자세히 알아보려면 [Azure Active Directory 개발자 가이드](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-148">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="a8c0f-149">응용 프로그램의 Single Sign-On 모드를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="a8c0f-149">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="a8c0f-150">응용 프로그램의 **Single Sign-On** 모드를 설정하려면 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-150">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="a8c0f-151">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8c0f-152">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8c0f-153">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8c0f-154">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8c0f-155">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a8c0f-156">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8c0f-157">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-157">Select the application for which you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="a8c0f-158">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-158">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="how-to-choose-a-provisioning-mode"></a><span data-ttu-id="a8c0f-159">프로비전 모드를 선택하는 방법</span><span class="sxs-lookup"><span data-stu-id="a8c0f-159">How to choose a provisioning mode</span></span>

-   <span data-ttu-id="a8c0f-160">**수동 프로비전** - 기존 계정이 있거나 Azure AD 외부에서 이 응용 프로그램에 대한 계정을 관리하려는 경우 [수동](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) 프로비전 모드 선택</span><span class="sxs-lookup"><span data-stu-id="a8c0f-160">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="a8c0f-161">**자동 프로비전** - 자동 API 기반 프로비전 및/또는 이 응용 프로그램에 사용자 계정의 프로비전 해제를 활성화하려면 [자동](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **프로비전 모드** 선택</span><span class="sxs-lookup"><span data-stu-id="a8c0f-161">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="a8c0f-162">이 옵션은 [Azure AD 응용 프로그램 갤러리](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery)의 **주요** 범주 내의 응용 프로그램에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-162">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="a8c0f-163">**SCIM 기반 자동 프로비전** - 응용 프로그램이 Azure AD와 통합된 모든 응용 프로그램에 변경 내용을 자동으로 내보내는 사용자 및 그룹에 대한 변경 내용 감지에 SCIM 프로토콜을 지원하는 경우 [SCIM 기반 자동 프로비전](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) 사용</span><span class="sxs-lookup"><span data-stu-id="a8c0f-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="a8c0f-164">이 옵션은 특정 프로비전 모드로 나열되어 있지 않지만 Azure AD와 통합된 모든 응용 프로그램에 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-to-set-an-applications-provisioning-mode"></a><span data-ttu-id="a8c0f-165">응용 프로그램의 프로비전 모드를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="a8c0f-165">How to set an application’s provisioning mode</span></span>

<span data-ttu-id="a8c0f-166">응용 프로그램의 **프로비전** 모드를 설정하려면 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-166">To set an application’s **provisioning** mode, follow the instructions below:</span></span>

<span data-ttu-id="a8c0f-167">응용 프로그램의 **Single Sign-On** 모드를 설정하려면 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-167">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="a8c0f-168">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8c0f-169">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8c0f-170">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8c0f-171">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8c0f-172">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-172">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a8c0f-173">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a8c0f-174">프로비전을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-174">Select the application for which you want to configure provisioning.</span></span>

7.  <span data-ttu-id="a8c0f-175">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **프로비전**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c0f-175">Once the application loads, click **Provisioning** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8c0f-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8c0f-176">Next steps</span></span>
[<span data-ttu-id="a8c0f-177">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="a8c0f-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
