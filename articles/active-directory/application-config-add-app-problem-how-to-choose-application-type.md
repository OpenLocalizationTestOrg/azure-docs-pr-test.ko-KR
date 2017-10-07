---
title: "응용 프로그램을 응용 프로그램을 추가할 때 toouse 입력 aaaHow toochoose | Microsoft Docs"
description: "지원 되는 hello 유형의 Azure AD와 통합할 수 있습니다 하는 응용 프로그램 이해 및 관련된 구성 옵션"
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
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a><span data-ttu-id="14646-103">어떻게 응용 프로그램을 응용 프로그램을 추가할 때 toouse 입력 toochoose</span><span class="sxs-lookup"><span data-stu-id="14646-103">How toochoose which application type toouse when adding an application</span></span>

<span data-ttu-id="14646-104">이 문서가 도움이 되었나요 toounderstand hello 라는 네 가지 종류의 응용 프로그램을 Azure AD와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-104">This article help you toounderstand hello four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="14646-105">각 형식에 의해 지원되는 항목</span><span class="sxs-lookup"><span data-stu-id="14646-105">What is supported by each of them</span></span>
* <span data-ttu-id="14646-106">해당 응용 프로그램을 선택할 수도 있는 이유</span><span class="sxs-lookup"><span data-stu-id="14646-106">Why you might choose which application</span></span>
* <span data-ttu-id="14646-107">어떻게 tooconfigure 해당 응용 프로그램의 핵심 속성 같은 사용자가 방법을 **프로 비전**, 기능 또는 **단일 로그온** 기술 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-107">How tooconfigure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology toouse.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="14646-108">Azure AD에서 지원되는 응용 프로그램 형식</span><span class="sxs-lookup"><span data-stu-id="14646-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="14646-109">Azure AD에서는 4 개의 주 응용 프로그램 유형을 사용 하 여 추가할 수 있는 hello **추가** 기능을 확인할 **엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-109">Azure AD supports four main application types that you can add using hello **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="14646-110">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-110">These include:</span></span>

-   <span data-ttu-id="14646-111">**Azure AD 갤러리 응용 프로그램** – Single Sign-On에 대해 Azure AD와 사전 통합된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="14646-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="14646-112">**응용 프로그램 프록시 응용 프로그램** – tooprovide 보안 single sign-on tooexternally 원하는 온-프레미스 환경에서 실행 중인 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="14646-112">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

-   <span data-ttu-id="14646-113">**사용자 지정 응용 프로그램 개발** – 조직에서 toodevelop 하지 않고자 한다면 응용 프로그램에 Azure AD 응용 프로그램 개발 플랫폼 hello 하지만 아직 존재 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-113">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="14646-114">**비 갤러리 응용 프로그램** – 사용자의 응용 프로그램을 가져옵니다!</span><span class="sxs-lookup"><span data-stu-id="14646-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="14646-115">원하는 모든 웹 링크 또는 사용자 이름 및 암호 필드를 렌더링 하는 응용 프로그램에는 SAML 또는 OpenID Connect 프로토콜을 지원 또는 Azure ad에서 single sign-on toointegrate 복원할 SCIM를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a><span data-ttu-id="14646-116">기능 및 응용 프로그램 종류 위의 모든 hello에서 지 원하는 기능</span><span class="sxs-lookup"><span data-stu-id="14646-116">Features and capabilities supported by all hello above application types</span></span>

<span data-ttu-id="14646-117">hello 다음과 같은 기능이 지원 됩니다 hello 위의 4 응용 프로그램 종류의 Azure AD에서.</span><span class="sxs-lookup"><span data-stu-id="14646-117">hello following features are supported by any of hello above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="14646-118">**빠른 시작** – [간단한 배포 단계](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)를 수행하여 신속하게 응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="14646-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="14646-119">**일반 속성 관리** -가져오기는 [직접 딥 링크](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan 응용 프로그램 [hello 브랜딩 사용자 지정](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) 응용 프로그램의 또는 [hello응용프로그램을사용하지않도록설정](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) 모든 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan application, [customize hello branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable hello application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="14646-120">**사용자 및 그룹 관리** – [할당](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) 또는 [제거](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) tooan 응용 프로그램을 사용자 및 그룹 및 필요에 따라이 사용자 및 그룹에 대 한 액세스 권한이 할당 hello 특정 응용 프로그램 역할</span><span class="sxs-lookup"><span data-stu-id="14646-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups tooan application, and optionally assign hello specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="14646-121">**셀프 서비스 응용 프로그램 액세스** – 사용자가 toorequest 활성화 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan 응용 프로그램에서 해당 응용 프로그램 액세스 패널 응용 프로그램을 직접 추가 하 여 하나 또는 [ 셀프 서비스 활성화 된 그룹에 가입](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), 선택적으로 hello 따라 비즈니스 승인이 필요한 방식으로</span><span class="sxs-lookup"><span data-stu-id="14646-121">**Self-service application access** – enable your users toorequest [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along hello way</span></span>

-   <span data-ttu-id="14646-122">**로그인 로그가** – 참조 [로그인 tooan 응용 프로그램을 hello 모든](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), 또는 모든 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="14646-122">**Sign-in logs** – see [all hello sign-ins tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="14646-123">**감사 로그** – 참조 [수정 tooan 응용 프로그램에 대 한 감사 로그 세부](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), 또는 tooall 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="14646-123">**Audit logs** – see [detailed audit logs about modifications tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or tooall your applications</span></span>

-   <span data-ttu-id="14646-124">**조건부 및 위험 기반 액세스** 강력한 설정 – [조건 기반 액세스 규칙](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) toosign tooa 특정 응용 프로그램에서 사용자가 때 적용 되는</span><span class="sxs-lookup"><span data-stu-id="14646-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt toosign in tooa specific application</span></span>

-   <span data-ttu-id="14646-125">**권한 보기** – hello의 [OAuth2 권한](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) 응용 프로그램은 액세스 tooin 디렉터리 한 곳에서</span><span class="sxs-lookup"><span data-stu-id="14646-125">**Permissions view** – view any of hello [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access tooin your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="14646-126">특정 응용 프로그램 형식에서 지원되는 Single Sign-On 및 프로비전 모드</span><span class="sxs-lookup"><span data-stu-id="14646-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="14646-127">hello 표에서 hello 다른 single sign on 및 각 응용 프로그램 종류 위에 hello에서 지 원하는 모드 프로 비전을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-127">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="14646-128">이 테이블 toohelp를 사용할 수 있습니다 toounderstand 필요한 응용 프로그램을 tooadd toosupport 구체적인 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="14646-128">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![앱 형식 테이블](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="14646-130">어떻게 toochoose single sign on 모드</span><span class="sxs-lookup"><span data-stu-id="14646-130">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="14646-131">지원 되는 hello **단일 로그온** Azure AD 응용 프로그램에 대 한 모드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-131">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="14646-132">**Azure AD에서 single sign-on 사용 하지 않도록 설정** – Azure AD에서 single sign-on 사용 하지 않도록 설정 선택 **single sign on 모드** 아직 준비 되지 않음 toointegrate로 Azure ad에서 single sign이 응용이 프로그램은 또는 아웃 테스트 하기만 하는 경우</span><span class="sxs-lookup"><span data-stu-id="14646-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="14646-133">**로그온 연결** – hello 선택 [연결 된 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign on 모드** 는 기존 single sign-on 솔루션와 이미 연결 된 응용 프로그램이 있는 경우 또는 원하는 경우 에 있는 사용자에 대 한 링크는 간단한 toopublish 자신의 [응용 프로그램 액세스 패널로](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) 또는 [Office 365 응용 프로그램 실행 프로그램](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="14646-133">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="14646-134">**암호 기반 로그온** – hello 선택 [암호 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign on 모드** 응용 프로그램 HTML 사용자 이름 및 암호 필드를 렌더링 하 고 toostore입니다 사용자 이름 및 암호 안전 하 게 toobe 재생 나중에 toohello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="14646-134">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="14646-135">**SAML 기반 로그온** – hello 선택 [SAML 기반 로그온](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) 응용 프로그램 hello SAML 또는 OpenID Connect 프로토콜을 지원 하거나 toobe 수 toomap 사용자 모드에서 single sign toospecific 응용 프로그램 역할 기반 saml 사용자 정의 규칙 클레임 *</span><span class="sxs-lookup"><span data-stu-id="14646-135">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="14646-136">Hello 응용 프로그램 프록시 응용 프로그램에 대해 구성 된 경우에이 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-136">This option is not available when hello application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="14646-137">**머리글 기반 로그온** –이 옵션을 선택 [헤더 기반 로그온](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign on 모드 PingAccess 지 원하는 HTTP 헤더를 사용 하 여 응용 프로그램이 있는 경우 기반 인증을 tooperform 단일 기호에 너무</span><span class="sxs-lookup"><span data-stu-id="14646-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="14646-138">이 옵션은 응용 프로그램 프록시와 PingAccess hello 응용 프로그램에 대해 구성 된 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-138">This option is only available when hello application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="14646-139">**Windows 통합 인증을** – hello 선택 [Windows 통합 인증](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single sign-on 모드를 원하는 tooperform 단일 기호에 너무 하는 온-프레미스 WIA 응용 프로그램을 노출 하는 경우</span><span class="sxs-lookup"><span data-stu-id="14646-139">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="14646-140">이 옵션은 hello 응용 프로그램 프록시 응용 프로그램에 대해 구성 된 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-140">This option is only available when hello application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="14646-141">사용자 지정 개발된 응용 프로그램에 대한 Single Sign-On 모드</span><span class="sxs-lookup"><span data-stu-id="14646-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="14646-142">Hello 통해 개발 하는 사용자 지정 수 있는 응용 프로그램 [응용 프로그램 사용자 지정 개발](#_Custom-Developed_Applications) 환경에 추가 single sign on 모드 위에 나열 되지 않은 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-142">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="14646-143">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-143">These include:</span></span>

-   <span data-ttu-id="14646-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="14646-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="14646-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="14646-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="14646-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="14646-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="14646-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 기반 로그온</span><span class="sxs-lookup"><span data-stu-id="14646-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="14646-148">읽기 hello [Azure Active Directory 개발자 가이드](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn 어떻게는 이러한 사용자 지정 개발 toocreate 응용 프로그램 single sign on 모드에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-148">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="14646-149">어떻게 tooset 응용 프로그램의 single sign on 모드</span><span class="sxs-lookup"><span data-stu-id="14646-149">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="14646-150">tooset 응용 프로그램의 **단일 로그온** 아래 지침에 따라 hello 모드:</span><span class="sxs-lookup"><span data-stu-id="14646-150">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="14646-151">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="14646-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="14646-152">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="14646-153">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="14646-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="14646-154">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="14646-155">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="14646-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="14646-156">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="14646-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="14646-157">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-157">Select hello application for which you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="14646-158">Hello 응용 프로그램 로드 되 면 클릭 **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-158">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="how-toochoose-a-provisioning-mode"></a><span data-ttu-id="14646-159">어떻게 toochoose 프로비저닝 모드</span><span class="sxs-lookup"><span data-stu-id="14646-159">How toochoose a provisioning mode</span></span>

-   <span data-ttu-id="14646-160">**수동 프로 비전** – hello 선택 [수동](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) 기존 계정이 있는 또는 외부 Azure AD에서이 응용 프로그램에 대 한 toomanage 계정을 지정할 경우 프로 비전 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="14646-160">**Manual Provisioning** – choose hello [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish toomanage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="14646-161">**자동 프로 비전** – hello 선택 [자동](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **프로비저닝 모드** 사용자 계정을 toothis tooenable 자동 API 기반 프로 비전 및/또는의 프로 비전 해제 하려는 경우 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="14646-161">**Automatic Provisioning** – choose hello [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want tooenable automatic API-based provisioning and/or de-provisioning of user accounts toothis application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="14646-162">이 옵션은 hello 내에서 응용 프로그램에 대해서만 사용할 수 있는 **갖춘** hello 범주의 [Azure AD 응용 프로그램 갤러리](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery)합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-162">This option is available only for applications within hello **featured** category of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="14646-163">**자동 프로 비전 SCIM 기반** – 사용 하 여 [SCIM 기반 자동 프로 비전](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) 응용 프로그램 변경 내용 toousers 및 변경 내용에 대해 자동으로 내보내는 그룹 검색에 대 한 hello SCIM 프로토콜을 지 원하는 경우 Azure AD와 통합 tooany 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="14646-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports hello SCIM protocol for detecting changes toousers and groups, which are automatically emitted for changes tooany application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="14646-164">이 옵션은 특정 프로비전 모드로 나열되어 있지 않지만 Azure AD와 통합된 모든 응용 프로그램에 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="14646-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a><span data-ttu-id="14646-165">어떻게 tooset 응용 프로그램의 프로 비전 모드</span><span class="sxs-lookup"><span data-stu-id="14646-165">How tooset an application’s provisioning mode</span></span>

<span data-ttu-id="14646-166">tooset 응용 프로그램의 **프로 비전** 아래 지침에 따라 hello 모드:</span><span class="sxs-lookup"><span data-stu-id="14646-166">tooset an application’s **provisioning** mode, follow hello instructions below:</span></span>

<span data-ttu-id="14646-167">tooset 응용 프로그램의 **단일 로그온** 아래 지침에 따라 hello 모드:</span><span class="sxs-lookup"><span data-stu-id="14646-167">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="14646-168">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="14646-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="14646-169">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14646-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="14646-170">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="14646-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="14646-171">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="14646-172">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="14646-172">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="14646-173">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="14646-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="14646-174">Tooconfigure 프로 비전 하려는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-174">Select hello application for which you want tooconfigure provisioning.</span></span>

7.  <span data-ttu-id="14646-175">Hello 응용 프로그램 로드 되 면 클릭 **프로 비전** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="14646-175">Once hello application loads, click **Provisioning** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14646-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="14646-176">Next steps</span></span>
[<span data-ttu-id="14646-177">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="14646-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
