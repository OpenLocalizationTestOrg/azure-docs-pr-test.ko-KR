---
title: "Azure AD Connect: 통과 인증 - 현재 제한 사항 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory (Azure AD) 통과 인증의 hello 현재 제한 설명 합니다."
services: active-directory
keywords: "Azure AD Connect 통과 인증, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="d578c-104">Azure Active Directory 통과 인증: 현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="d578c-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="d578c-105">Azure AD 통과 인증은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="d578c-106">사용 가능한 기능 및 모든 유료 버전의 Azure AD toouse 필요 하지 않습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-106">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="d578c-107">통과 인증 에서만 사용 가능 hello 전세계 인스턴스는 Azure AD와 아닌에서 [Microsoft 클라우드 독일](http://www.microsoft.de/cloud-deutschland) 및 [Microsoft Azure Government 클라우드](https://azure.microsoft.com/features/gov/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-107">Pass-through Authentication is only available in hello world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="d578c-108">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="d578c-108">Supported scenarios</span></span>

<span data-ttu-id="d578c-109">다음 시나리오는 hello은 미리 보기 중 완전히 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-109">hello following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="d578c-110">사용자가 모든 웹 브라우저 기반 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="d578c-111">사용자가 [최신 인증](https://aka.ms/modernauthga)을 지원하는 Office 365 클라이언트 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="d578c-112">Windows 10 장치에 대한 Azure AD 조인.</span><span class="sxs-lookup"><span data-stu-id="d578c-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="d578c-113">Exchange ActiveSync 지원.</span><span class="sxs-lookup"><span data-stu-id="d578c-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="d578c-114">지원되지 않는 시나리오</span><span class="sxs-lookup"><span data-stu-id="d578c-114">Unsupported scenarios</span></span>

<span data-ttu-id="d578c-115">hello 다음과 같은 시나리오를 _하지_ 미리 보기 기간 동안 지원:</span><span class="sxs-lookup"><span data-stu-id="d578c-115">hello following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="d578c-116">사용자는 레거시 Office 클라이언트 응용 프로그램(Office 2013 이전 버전)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="d578c-117">조직에서는 잘된 tooswitch toomodern 인증을 가능 하면 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-117">Organizations are encouraged tooswitch toomodern authentication, if possible.</span></span> <span data-ttu-id="d578c-118">최신 인증을 사용하면 통과 인증 지원이 허용될 뿐 아니라 MFA(Multi-Factor Authentication) 등의 [조건부 액세스](../active-directory-conditional-access.md) 기능을 사용하여 사용자 계정을 보호할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="d578c-119">사용자가 비즈니스용 Skype 2016을 포함한 비즈니스용 Skype 클라이언트 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="d578c-120">사용자가 PowerShell v1.0에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="d578c-121">PowerShell v2.0을 대신 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d578c-122">지원 되지 않는 시나리오에 대 한 해결 방법으로 암호 해시 동기화 hello에서 사용 하도록 설정 [선택적 기능](active-directory-aadconnect-get-started-custom.md#optional-features) hello Azure AD Connect 마법사의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on hello [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in hello Azure AD Connect wizard.</span></span> <span data-ttu-id="d578c-123">이전 시나리오 hello에 대 한 대체 방식으로 암호 해시 동기화 역할 _만_ (및 _하지_ 제네릭 대체 인증 방법으로 tooPass 통해).</span><span class="sxs-lookup"><span data-stu-id="d578c-123">Password Hash Synchronization acts as a fallback for hello preceding scenarios _only_ (and _not_ as a generic fallback tooPass-through Authentication).</span></span> <span data-ttu-id="d578c-124">이러한 시나리오가 필요하지 않으면 암호 해시 동기화를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d578c-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d578c-125">Next steps</span></span>
- <span data-ttu-id="d578c-126">[**빠른 시작**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Azure AD 통과 인증을 작동하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="d578c-127">[**기술 심층 분석**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="d578c-128">[**질문과 대답** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 질문과 대답을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="d578c-129">[**문제를 해결** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="d578c-130">[**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="d578c-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="d578c-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
