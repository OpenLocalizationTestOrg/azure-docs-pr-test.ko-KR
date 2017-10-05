---
title: "Azure Active Directory 응용 프로그램 갤러리에 응용 프로그램 나열"
description: "Azure Active Directory 갤러리에서 Single Sign-On을 지원하는 응용 프로그램을 나열하는 방법 | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: cf25772bd9d92b59401aa5da76e6bbd5fa5ee3e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="listing-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="33e18-103">Azure Active Directory 응용 프로그램 갤러리에 응용 프로그램 나열</span><span class="sxs-lookup"><span data-stu-id="33e18-103">Listing your application in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="33e18-104">[Azure AD 갤러리](https://azure.microsoft.com/marketplace/active-directory/all/)에서 Azure Active Directory를 사용하여 Single Sign-On을 지원하는 응용 프로그램을 나열하려면 먼저 응용 프로그램은 다음의 통합 모드 중 하나를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span></span>

* <span data-ttu-id="33e18-105">**OpenID Connect** - 인증을 위한 OpenID Connect 및 구성을 위한 Azure AD 동의 API를 사용하는 Azure AD과 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="33e18-106">통합을 시작하고 응용 프로그램이 SAML을 지원하지 않으면 이것이 권장 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
* <span data-ttu-id="33e18-107">**SAML** – 응용 프로그램에는 이미 SAML 프로토콜을 사용하여 타사 ID 공급자를 구성할 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="33e18-108">각 모드에 대한 요구 사항을 나열하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="33e18-109">OpenID Connect 통합</span><span class="sxs-lookup"><span data-stu-id="33e18-109">OpenID Connect Integration</span></span>
<span data-ttu-id="33e18-110">응용 프로그램과 Azure AD를 통합하려면 [개발자 지침](active-directory-authentication-scenarios.md)을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="33e18-111">그런 다음 아래 질문을 완료하여 waadpartners@microsoft.com으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-111">Then complete the questions below and send to waadpartners@microsoft.com.</span></span>

* <span data-ttu-id="33e18-112">Azure AD 팀에서 사용할 수 있는 응용 프로그램을 사용하는 테스트 테넌트 또는 계정에 대한 자격 증명을 제공하여 통합을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="33e18-113">Azure AD 팀이 [Azure AD 동의 프레임워크](active-directory-integrating-applications.md#overview-of-the-consent-framework)를 사용하여 로그인하고 응용 프로그램에 Azure AD의 인스턴스를 연결하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="33e18-114">응용 프로그램을 사용하여 Single Sign-On을 테스트하기 위해 Azure AD 팀에 필요한 추가 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span></span> 
* <span data-ttu-id="33e18-115">아래의 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-115">Provide the info below:</span></span>

> <span data-ttu-id="33e18-116">회사 이름:</span><span class="sxs-lookup"><span data-stu-id="33e18-116">Company Name:</span></span>
> 
> <span data-ttu-id="33e18-117">회사 웹 사이트:</span><span class="sxs-lookup"><span data-stu-id="33e18-117">Company Website:</span></span>
> 
> <span data-ttu-id="33e18-118">응용 프로그램 이름:</span><span class="sxs-lookup"><span data-stu-id="33e18-118">Application Name:</span></span>
> 
> <span data-ttu-id="33e18-119">응용 프로그램 설명(200자 제한):</span><span class="sxs-lookup"><span data-stu-id="33e18-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="33e18-120">응용 프로그램 웹 사이트 (정보):</span><span class="sxs-lookup"><span data-stu-id="33e18-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="33e18-121">응용 프로그램 기술 지원 웹 사이트 또는 연락처 정보:</span><span class="sxs-lookup"><span data-stu-id="33e18-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="33e18-122">https://portal.azure.com의 응용 프로그램 세부 정보에 표시된 응용 프로그램의 응용 프로그램 ID:</span><span class="sxs-lookup"><span data-stu-id="33e18-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="33e18-123">고객이 응용 프로그램에 등록하거나 구입하기 위해 이동하는 응용 프로그램 등록 URL:</span><span class="sxs-lookup"><span data-stu-id="33e18-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="33e18-124">응용 프로그램을 나열할 범주를 최대 세 가지 선택합니다.(사용 가능한 범주는 Azure Active Directory 마켓플레이스 참조)</span><span class="sxs-lookup"><span data-stu-id="33e18-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="33e18-125">응용 프로그램 연결 작은 아이콘(PNG 파일, 45x45px, 단색 배경):</span><span class="sxs-lookup"><span data-stu-id="33e18-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="33e18-126">응용 프로그램 연결 큰 아이콘(PNG 파일, 215x215px, 단색 배경):</span><span class="sxs-lookup"><span data-stu-id="33e18-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="33e18-127">응용 프로그램 연결 로고(PNG 파일, 150x122px, 투명 배경색):</span><span class="sxs-lookup"><span data-stu-id="33e18-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="33e18-128">SAML 통합</span><span class="sxs-lookup"><span data-stu-id="33e18-128">SAML Integration</span></span>
<span data-ttu-id="33e18-129">SAML 2.0을 지원하는 앱은 [사용자 지정 응용 프로그램을 추가하기 위해 다음 지침](../active-directory-saas-custom-apps.md)을 사용하여 Azure AD 테넌트로 직접 통합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="33e18-130">응용 프로그램 통합이 Azure AD를 사용하여 작동하는지 테스트하면 다음 정보를 <mailto:waadpartners@microsoft.com>로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="33e18-131">Azure AD 팀에서 사용할 수 있는 응용 프로그램을 사용하는 테스트 테넌트 또는 계정에 대한 자격 증명을 제공하여 통합을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="33e18-132">[여기](../active-directory-saas-custom-apps.md)에 설명한 대로 응용 프로그램에 대한 SAML 로그온 URL, 발급자 URL(엔터티 ID) 및 회신 URL(어설션 소비자 서비스) 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="33e18-133">일반적으로 SAML 메타데이터 파일의 일부로 이러한 값을 제공하는 경우 또한 해당 파일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="33e18-134">SAML 2.0을 사용하여 응용 프로그램에서 Azure AD를 ID 공급자로 구성하는 방법에 대한 간략한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="33e18-135">응용 프로그램에서 셀프 서비스 관리 포털을 통해 Azure AD를 ID 공급자로 구성하도록 지원하는 경우 위에 제공된 자격 증명이 이를 설정할 기능을 포함하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span></span>
* <span data-ttu-id="33e18-136">아래의 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33e18-136">Provide the info below:</span></span>

> <span data-ttu-id="33e18-137">회사 이름:</span><span class="sxs-lookup"><span data-stu-id="33e18-137">Company Name:</span></span>
> 
> <span data-ttu-id="33e18-138">회사 웹 사이트:</span><span class="sxs-lookup"><span data-stu-id="33e18-138">Company Website:</span></span>
> 
> <span data-ttu-id="33e18-139">응용 프로그램 이름:</span><span class="sxs-lookup"><span data-stu-id="33e18-139">Application Name:</span></span>
> 
> <span data-ttu-id="33e18-140">응용 프로그램 설명(200자 제한):</span><span class="sxs-lookup"><span data-stu-id="33e18-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="33e18-141">응용 프로그램 웹 사이트 (정보):</span><span class="sxs-lookup"><span data-stu-id="33e18-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="33e18-142">응용 프로그램 기술 지원 웹 사이트 또는 연락처 정보:</span><span class="sxs-lookup"><span data-stu-id="33e18-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="33e18-143">고객이 응용 프로그램에 등록하거나 구입하기 위해 이동하는 응용 프로그램 등록 URL:</span><span class="sxs-lookup"><span data-stu-id="33e18-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="33e18-144">응용 프로그램을 나열할 범주를 최대 세 가지 선택합니다(사용 가능한 범주는 [Azure Active Directory 마켓플레이스](https://azure.microsoft.com/marketplace/active-directory/)참조).</span><span class="sxs-lookup"><span data-stu-id="33e18-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="33e18-145">응용 프로그램 연결 작은 아이콘(PNG 파일, 45x45px, 단색 배경):</span><span class="sxs-lookup"><span data-stu-id="33e18-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="33e18-146">응용 프로그램 연결 큰 아이콘(PNG 파일, 215x215px, 단색 배경):</span><span class="sxs-lookup"><span data-stu-id="33e18-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="33e18-147">응용 프로그램 연결 로고(PNG 파일, 150x122px, 투명 배경색):</span><span class="sxs-lookup"><span data-stu-id="33e18-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

