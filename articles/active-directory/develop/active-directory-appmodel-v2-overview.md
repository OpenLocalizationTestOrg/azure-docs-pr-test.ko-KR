---
title: "Azure Active Directory v2.0 끝점 | Microsoft Docs"
description: "Microsoft 계정 및 Azure Active Directory 로그인을 사용하는 앱 구축을 소개합니다."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1e286044fb1a1b367fcac2dc14c47f68d5ed120d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="af5c3-103">단일 앱에서 Microsoft 계정 및 Azure AD 사용자 로그인</span><span class="sxs-lookup"><span data-stu-id="af5c3-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="af5c3-104">과거 Azure Active Directory에서 Microsoft 개인 계정과 회사 계정을 모두 지원하려는 앱 개발자는 별도의 두 시스템과 통합해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-104">In the past, an app developer who wanted to support both personal Microsoft accounts and work accounts from Azure Active Directory was required to integrate with two separate systems.</span></span>  <span data-ttu-id="af5c3-105">**Azure AD v2.0 끝점**에서는 간단한 통합을 사용하여 두 가지 유형의 계정에 모두 로그인할 수 있게 하는 새로운 인증 API 버전을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-105">The **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you to sign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="af5c3-106">또한 v2.0 끝점을 사용하는 앱은 두 가지 계정 유형 중 하나를 사용하여 [Microsoft Graph](https://graph.microsoft.io)에서 REST API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-106">Apps that use the v2.0 endpoint can also consume REST APIs from the [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="af5c3-107">시작하기</span><span class="sxs-lookup"><span data-stu-id="af5c3-107">Getting Started</span></span>
<span data-ttu-id="af5c3-108">다음 목록에서 원하는 플랫폼을 선택하여 당사의 오픈 소스 라이브러리 및 프레임워크를 사용하여 앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-108">Choose your favorite platform from the following list to build an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="af5c3-109">또는 인증 라이브러리를 사용하지 않고 당사의 OAuth 2.0 및 OpenID Connect 프로토콜 설명서를 사용하여 프로토콜 메시지를 직접 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation to send & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="af5c3-110">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="af5c3-110">What's New</span></span>
<span data-ttu-id="af5c3-111">여기서 설명하는 정보는 v2.0 끝점을 통해 가능한 작업과 불가능한 작업을 이해하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-111">The information here will be useful in understanding what is & what isn't possible with the v2.0 endpoint.</span></span>

* <span data-ttu-id="af5c3-112">[v2.0 끝점을 사용하여 만들 수 있는 앱의 종류](active-directory-v2-flows.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-112">Learn about the [types of apps you can build with the v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="af5c3-113">v2.0 끝점에 대한 [제한, 제한 사항 및 제약 조건](active-directory-v2-limitations.md) 을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-113">Understand the [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with the v2.0 endpoint.</span></span>
* <span data-ttu-id="af5c3-114">v2.0 끝점에 대해 다음 개요 비디오를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-114">Check out this overview video for the v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="af5c3-115">참조</span><span class="sxs-lookup"><span data-stu-id="af5c3-115">Reference</span></span>
<span data-ttu-id="af5c3-116">이러한 링크는 플랫폼을 자세히 탐색하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-116">These links will be useful for exploring the platform in depth:</span></span>

* [<span data-ttu-id="af5c3-117">v2.0 프로토콜 참조</span><span class="sxs-lookup"><span data-stu-id="af5c3-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="af5c3-118">v2.0 토큰 참조</span><span class="sxs-lookup"><span data-stu-id="af5c3-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="af5c3-119">v2.0 라이브러리 참조</span><span class="sxs-lookup"><span data-stu-id="af5c3-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="af5c3-120">v2.0 끝점의 범위 및 동의</span><span class="sxs-lookup"><span data-stu-id="af5c3-120">Scopes and Consent in the v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="af5c3-121">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="af5c3-121">The Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="af5c3-122">도움말 및 지원</span><span class="sxs-lookup"><span data-stu-id="af5c3-122">Help & Support</span></span>
<span data-ttu-id="af5c3-123">Azure Active Directory 개발과 관련하여 도움을 받기에 가장 좋은 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-123">These are the best places to get help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="af5c3-124">Stack Overflow`azure-active-directory` 및 `adal` 태그</span><span class="sxs-lookup"><span data-stu-id="af5c3-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="af5c3-125">Azure Active Directory에 대한 피드백</span><span class="sxs-lookup"><span data-stu-id="af5c3-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="af5c3-126">Azure Active Directory에서 회사 계정과 학교 계정에만 로그인해야 하는 경우 [개발자용 Azure AD 가이드](active-directory-developers-guide.md)를 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-126">If you only need to sign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="af5c3-127">v2.0 끝점은 Microsoft 개인 계정에 명시적으로 로그인해야 하는 개발자가 사용하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="af5c3-127">The v2.0 endpoint is intended for use by developers who explicitly need to sign in Microsoft personal accounts.</span></span>

