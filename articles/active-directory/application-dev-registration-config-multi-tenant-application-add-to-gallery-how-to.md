---
title: "다중 테 넌 트 응용 프로그램 toohello Azure AD 응용 프로그램 갤러리 aaaHow tooadd | Microsoft Docs"
description: "Hello Azure AD 응용 프로그램 갤러리에서에서 사용자 지정 개발 된 다중 테 넌 트 응용 프로그램을 나열할 수는 방법에 대해 설명"
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
ms.openlocfilehash: 2dc6e0d783835d2639a7e6dda172110ee860a977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-multi-tenant-application-toohello-azure-ad-application-gallery"></a><span data-ttu-id="d2d65-103">어떻게 tooadd 다중 테 넌 트 응용 프로그램 toohello Azure AD 응용 프로그램 갤러리</span><span class="sxs-lookup"><span data-stu-id="d2d65-103">How tooadd a multi-tenant application toohello Azure AD application gallery</span></span>

## <a name="what-is-hello-azure-ad-application-gallery"></a><span data-ttu-id="d2d65-104">Hello Azure AD 응용 프로그램 갤러리 란?</span><span class="sxs-lookup"><span data-stu-id="d2d65-104">What is hello Azure AD Application Gallery?</span></span>

<span data-ttu-id="d2d65-105">hello Azure AD 응용 프로그램 갤러리 위한 훌륭한 방법 tooget 응용 프로그램을 모든 hello 수백만 앞에 Azure Active Directory 고객 toobroaden hello 영향 이며 hello 시장에서 응용 프로그램의 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d65-105">hello Azure AD Application Gallery is a great way tooget your application in front of all hello millions of Azure Active Directory customers toobroaden hello impact and reach of your application in hello marketplace.</span></span> <span data-ttu-id="d2d65-106">아래 단계는 hello hello Azure AD 응용 프로그램 갤러리에서에서 응용 프로그램을 나열할 수는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d65-106">hello below steps explain how you can list your application in hello Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="d2d65-107">응용 프로그램이 SAML 또는 OpenIDConnect를 지원하는 경우</span><span class="sxs-lookup"><span data-stu-id="d2d65-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="d2d65-108">Toolist hello Azure AD 응용 프로그램 갤러리에서에서 선택 하는 다중 테 넌 트 응용 프로그램의 경우 응용 프로그램 hello single sign on 기술 다음 중 하나를 지원 하는지 먼저 확인 해야 하면:</span><span class="sxs-lookup"><span data-stu-id="d2d65-108">If you have a multi-tenant application you'd like toolist in hello Azure AD Application Gallery, you must first make sure that your application supports one of hello following single sign-on technologies:</span></span>

1. <span data-ttu-id="d2d65-109">**OpenID Connect** -OpenID Connect를 사용 하 여 인증을 위해 Azure AD와 직접 통합 하 고 구성에 대 한 Azure AD 동의 API hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d65-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="d2d65-110">통합 시작 하는 경우 응용 프로그램 SAML을 지원 하지 않는 hello 권장 되는 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2d65-110">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
2. <span data-ttu-id="d2d65-111">**SAML** – 응용 프로그램에 이미 hello SAML 프로토콜을 사용 하 여 hello 기능 tooconfigure 타사 id 공급자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d65-111">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="d2d65-112">응용 프로그램에서 single sign on 모드 중 하나를 지원 하 고 원하는 toolist hello Azure AD 응용 프로그램 갤러리에서에서 다중 테 넌 트 응용 프로그램 아래 hello 문서의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d65-112">If your application supports one of these single sign-on modes and you'd like toolist your multi-tenant application in hello Azure AD Application Gallery, you can follow hello steps in hello document below.</span></span> <span data-ttu-id="d2d65-113">빠르게 시작 tooget 너무 전자 메일을 보내**waadpartners@microsoft.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d65-113">tooget started quickly send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="d2d65-114">응용 프로그램이 SAML 또는 OpenIDConnect를 지원하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="d2d65-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="d2d65-115">응용 프로그램이 이러한 모드 중 하나를 지원하지 않더라도 암호 Single Sign-On 기술을 사용하여 갤러리에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2d65-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="d2d65-116">Tooexplore 원하는 경우이 옵션을 메일을 너무 보낼 수**waadpartners@microsoft.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2d65-116">If you'd like tooexplore this option, you can send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2d65-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2d65-117">Next steps</span></span>
[<span data-ttu-id="d2d65-118">어떻게 toolist hello Azure Active Directory 응용 프로그램 갤러리에서 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d2d65-118">How toolist your application in hello Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
