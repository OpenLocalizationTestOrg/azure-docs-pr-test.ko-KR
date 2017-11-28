---
title: "aaaAzure Active Directory v2.0 끝점 | Microsoft Docs"
description: "Microsoft 계정과 Azure Active Directory 로그인을 사용 하 여 소개 toobuilding 앱입니다."
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
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="7463b-103">단일 앱에서 Microsoft 계정 및 Azure AD 사용자 로그인</span><span class="sxs-lookup"><span data-stu-id="7463b-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="7463b-104">원하는 toosupport 두 개인 Microsoft 계정 앱 개발자 지나서 hello에 작업 계정을 Azure Active Directory에서 두 개의 별도 시스템과 필요한 toointegrate 되었으며 합니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="7463b-105">hello **Azure AD v2.0 끝점** toosign 유형에 서 모두 하나의 간단한 통합을 사용 하는 계정의 수 있는 새 인증 API 버전 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="7463b-106">Hello v2.0 끝점을 사용 하는 앱에서 hello 또한 REST Api를 사용할 수 [Microsoft Graph](https://graph.microsoft.io) 계정 유형 중 하나를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7463b-107">시작하기</span><span class="sxs-lookup"><span data-stu-id="7463b-107">Getting Started</span></span>
<span data-ttu-id="7463b-108">우리의 오픈 소스 라이브러리 및 프레임 워크를 사용 하 여 응용 프로그램 목록 toobuild 다음 hello에서 즐겨 찾는 플랫폼을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="7463b-109">또는 우리의 OAuth 2.0 및 OpenID Connect 프로토콜 설명서 toosend를 사용 하 여 & 인증 라이브러리를 사용 하지 않고 직접 프로토콜 메시지를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="7463b-110">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="7463b-110">What's New</span></span>
<span data-ttu-id="7463b-111">여기에 hello 정보는 이란 & hello v2.0 끝점과 수는 없습니다 기능 이해에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="7463b-112">Hello에 대 한 자세한 내용은 [유형의 hello v2.0 끝점을 빌드할 수 앱](active-directory-v2-flows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="7463b-113">Hello 이해 [제한 사항, 제한 사항 및 제약 조건](active-directory-v2-limitations.md) hello v2.0 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="7463b-114">이 개요 hello v2.0 끝점에 대 한 비디오 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="7463b-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="7463b-115">참조</span><span class="sxs-lookup"><span data-stu-id="7463b-115">Reference</span></span>
<span data-ttu-id="7463b-116">이러한 링크 심층에서 hello 플랫폼을 탐색 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="7463b-117">v2.0 프로토콜 참조</span><span class="sxs-lookup"><span data-stu-id="7463b-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="7463b-118">v2.0 토큰 참조</span><span class="sxs-lookup"><span data-stu-id="7463b-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="7463b-119">v2.0 라이브러리 참조</span><span class="sxs-lookup"><span data-stu-id="7463b-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="7463b-120">범위 및 hello v 2.0 끝점의 동의</span><span class="sxs-lookup"><span data-stu-id="7463b-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="7463b-121">Microsoft Graph hello</span><span class="sxs-lookup"><span data-stu-id="7463b-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="7463b-122">도움말 및 지원</span><span class="sxs-lookup"><span data-stu-id="7463b-122">Help & Support</span></span>
<span data-ttu-id="7463b-123">이들은 hello 최상의 위치 tooget 도움말을 보려면 Azure Active Directory에서 프로젝트를 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="7463b-124">Stack Overflow`azure-active-directory` 및 `adal` 태그</span><span class="sxs-lookup"><span data-stu-id="7463b-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="7463b-125">Azure Active Directory에 대한 피드백</span><span class="sxs-lookup"><span data-stu-id="7463b-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="7463b-126">로 시작 해야 toosign Azure Active Directory에서 회사 및 학교 계정에 필요한 경우 우리의 [Azure AD 개발자 가이드](active-directory-developers-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="7463b-127">hello v2.0 끝점 toosign 개인 Microsoft 계정에 명시적으로 해야 하는 개발자가 사용이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7463b-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>

