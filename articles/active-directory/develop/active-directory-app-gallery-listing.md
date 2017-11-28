---
title: "aaaListing hello Azure Active Directory 응용 프로그램 갤러리에서 응용 프로그램"
description: "Toolist single sign on에서 지 원하는 응용 프로그램의 Azure Active Directory 갤러리 hello 어떻게 | Microsoft Azure"
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
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="0c174-103">Hello Azure Active Directory 응용 프로그램 갤러리에서 응용 프로그램 나열</span><span class="sxs-lookup"><span data-stu-id="0c174-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="0c174-104">toolist 지 hello에서 single sign on Azure Active Directory와 원하는 응용 프로그램 [Azure AD 갤러리](https://azure.microsoft.com/marketplace/active-directory/all/), hello 응용 프로그램에는 먼저 hello 통합 모드를 다음 중 하나를 tooimplement 필요:</span><span class="sxs-lookup"><span data-stu-id="0c174-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="0c174-105">**OpenID Connect** -OpenID Connect를 사용 하 여 인증을 위해 Azure AD와 직접 통합 하 고 구성에 대 한 Azure AD 동의 API hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="0c174-106">통합 시작 하는 경우 응용 프로그램 SAML을 지원 하지 않는 hello 권장 되는 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="0c174-107">**SAML** – 응용 프로그램에 이미 hello SAML 프로토콜을 사용 하 여 hello 기능 tooconfigure 타사 id 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="0c174-108">각 모드에 대한 요구 사항을 나열하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="0c174-109">OpenID Connect 통합</span><span class="sxs-lookup"><span data-stu-id="0c174-109">OpenID Connect Integration</span></span>
<span data-ttu-id="0c174-110">toointegrate 다음 hello Azure AD와 응용 프로그램 [개발자 지침](active-directory-authentication-scenarios.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="0c174-111">그런 다음 아래 hello 질문을 완료 하 고 보낼 toowaadpartners@microsoft.com합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="0c174-112">Hello Azure AD 팀 tootest hello 통합 하 여 사용할 수 있는 응용 프로그램과 함께 테스트 테 넌 트 또는 계정에 대 한 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="0c174-113">Azure AD hello 팀 수에 로그인 하 고 hello를 사용 하 여 Azure AD tooyour 응용 프로그램의 인스턴스를 연결 하는 방법에 대 한 지침을 제공 [Azure AD의 승인 프레임 워크](active-directory-integrating-applications.md#overview-of-the-consent-framework)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="0c174-114">Tootest single sign on 응용 프로그램과 함께 팀 hello Azure AD에 필요한 추가 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="0c174-115">아래 hello 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-115">Provide hello info below:</span></span>

> <span data-ttu-id="0c174-116">회사 이름:</span><span class="sxs-lookup"><span data-stu-id="0c174-116">Company Name:</span></span>
> 
> <span data-ttu-id="0c174-117">회사 웹 사이트:</span><span class="sxs-lookup"><span data-stu-id="0c174-117">Company Website:</span></span>
> 
> <span data-ttu-id="0c174-118">응용 프로그램 이름:</span><span class="sxs-lookup"><span data-stu-id="0c174-118">Application Name:</span></span>
> 
> <span data-ttu-id="0c174-119">응용 프로그램 설명(200자 제한):</span><span class="sxs-lookup"><span data-stu-id="0c174-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="0c174-120">응용 프로그램 웹 사이트 (정보):</span><span class="sxs-lookup"><span data-stu-id="0c174-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="0c174-121">응용 프로그램 기술 지원 웹 사이트 또는 연락처 정보:</span><span class="sxs-lookup"><span data-stu-id="0c174-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="0c174-122">Https://portal.azure.com hello 응용 프로그램 세부 정보에 나와 있는 것 처럼 같은 hello 응용 프로그램의 응용 프로그램 ID:</span><span class="sxs-lookup"><span data-stu-id="0c174-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="0c174-123">응용 프로그램 등록 URL을 고객에 toosign 어디로 및/또는 구매 hello 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="0c174-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="0c174-124">(에 대 한 사용 가능한 범주 참조 hello Azure Active Directory Marketplace) 아래 나열 된 응용 프로그램 toobe 프로그램에 대 한 toothree 범주를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="0c174-125">응용 프로그램 연결 작은 아이콘(PNG 파일, 45x45px, 단색 배경):</span><span class="sxs-lookup"><span data-stu-id="0c174-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="0c174-126">응용 프로그램 연결 큰 아이콘(PNG 파일, 215x215px, 단색 배경):</span><span class="sxs-lookup"><span data-stu-id="0c174-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="0c174-127">응용 프로그램 연결 로고(PNG 파일, 150x122px, 투명 배경색):</span><span class="sxs-lookup"><span data-stu-id="0c174-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="0c174-128">SAML 통합</span><span class="sxs-lookup"><span data-stu-id="0c174-128">SAML Integration</span></span>
<span data-ttu-id="0c174-129">SAML 2.0을 지 원하는 모든 앱을 사용 하 여 Azure AD 테 넌 트와 직접 통합 될 수 있습니다 [이러한 지침 tooadd 사용자 지정 응용 프로그램](../active-directory-saas-custom-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="0c174-130">Azure AD와 응용 프로그램 통합을 작동 하는지 테스트 되 면 다음 정보를 너무 hello 전송할<mailto:waadpartners@microsoft.com>합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="0c174-131">Hello Azure AD 팀 tootest hello 통합 하 여 사용할 수 있는 응용 프로그램과 함께 테스트 테 넌 트 또는 계정에 대 한 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="0c174-132">설명 된 대로 SAML 로그온 URL, 발급자 URL (엔터티 ID), hello 및 회신 URL (어설션 소비자 서비스) 응용 프로그램에 대 한 값을 제공 [여기](../active-directory-saas-custom-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="0c174-133">일반적으로 SAML 메타데이터 파일의 일부로 이러한 값을 제공하는 경우 또한 해당 파일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="0c174-134">방법에 대 한 간략 한 설명을 제공 Azure AD SAML 2.0을 사용 하 여 응용 프로그램에 대 한 id 공급자로 tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="0c174-135">응용 프로그램에서 셀프 서비스 관리 포털을 통해를 id 공급자로 구성 Azure AD를 지 원하는 경우 다음 하십시오 위에 제공 된 hello 자격 증명 포함 확인 hello 기능 tooset를이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="0c174-136">아래 hello 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c174-136">Provide hello info below:</span></span>

> <span data-ttu-id="0c174-137">회사 이름:</span><span class="sxs-lookup"><span data-stu-id="0c174-137">Company Name:</span></span>
> 
> <span data-ttu-id="0c174-138">회사 웹 사이트:</span><span class="sxs-lookup"><span data-stu-id="0c174-138">Company Website:</span></span>
> 
> <span data-ttu-id="0c174-139">응용 프로그램 이름:</span><span class="sxs-lookup"><span data-stu-id="0c174-139">Application Name:</span></span>
> 
> <span data-ttu-id="0c174-140">응용 프로그램 설명(200자 제한):</span><span class="sxs-lookup"><span data-stu-id="0c174-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="0c174-141">응용 프로그램 웹 사이트 (정보):</span><span class="sxs-lookup"><span data-stu-id="0c174-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="0c174-142">응용 프로그램 기술 지원 웹 사이트 또는 연락처 정보:</span><span class="sxs-lookup"><span data-stu-id="0c174-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="0c174-143">응용 프로그램 등록 URL을 고객에 toosign 어디로 및/또는 구매 hello 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="0c174-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="0c174-144">아래 나열 된 응용 프로그램 toobe 프로그램에 대 한 toothree 범주를 선택 (사용 가능한 범주 참조 hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="0c174-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="0c174-145">응용 프로그램 연결 작은 아이콘(PNG 파일, 45x45px, 단색 배경):</span><span class="sxs-lookup"><span data-stu-id="0c174-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="0c174-146">응용 프로그램 연결 큰 아이콘(PNG 파일, 215x215px, 단색 배경):</span><span class="sxs-lookup"><span data-stu-id="0c174-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="0c174-147">응용 프로그램 연결 로고(PNG 파일, 150x122px, 투명 배경색):</span><span class="sxs-lookup"><span data-stu-id="0c174-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

