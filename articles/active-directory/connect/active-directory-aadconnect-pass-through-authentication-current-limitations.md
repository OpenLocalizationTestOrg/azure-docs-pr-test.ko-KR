---
title: "Azure AD Connect: 통과 인증 - 현재 제한 사항 | Microsoft Docs"
description: "이 문서에서는 Azure AD(Azure Active Directory) 통과 인증 문제의 현재 제한 사항에 대해 설명합니다."
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
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="860d1-104">Azure Active Directory 통과 인증: 현재 제한 사항</span><span class="sxs-lookup"><span data-stu-id="860d1-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="860d1-105">Azure AD 통과 인증은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="860d1-106">무료 기능이며 이 기능을 사용하는 데는 Azure AD 유료 버전이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-106">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="860d1-107">통과 인증은 Azure AD의 전 세계 인스턴스에서만 사용할 수 있고, [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) 및 [Microsoft Azure Government 클라우드](https://azure.microsoft.com/features/gov/)에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-107">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="860d1-108">지원되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="860d1-108">Supported scenarios</span></span>

<span data-ttu-id="860d1-109">다음 시나리오는 미리 보기 중에 완전히 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-109">The following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="860d1-110">사용자가 모든 웹 브라우저 기반 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="860d1-111">사용자가 [최신 인증](https://aka.ms/modernauthga)을 지원하는 Office 365 클라이언트 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="860d1-112">Windows 10 장치에 대한 Azure AD 조인.</span><span class="sxs-lookup"><span data-stu-id="860d1-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="860d1-113">Exchange ActiveSync 지원.</span><span class="sxs-lookup"><span data-stu-id="860d1-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="860d1-114">지원되지 않는 시나리오</span><span class="sxs-lookup"><span data-stu-id="860d1-114">Unsupported scenarios</span></span>

<span data-ttu-id="860d1-115">다음 시나리오는 미리 보기 중에 지원되지 _않습니다_.</span><span class="sxs-lookup"><span data-stu-id="860d1-115">The following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="860d1-116">사용자는 레거시 Office 클라이언트 응용 프로그램(Office 2013 이전 버전)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="860d1-117">가능할 경우 조직은 최신 인증으로 전환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-117">Organizations are encouraged to switch to modern authentication, if possible.</span></span> <span data-ttu-id="860d1-118">최신 인증을 사용하면 통과 인증 지원이 허용될 뿐 아니라 MFA(Multi-Factor Authentication) 등의 [조건부 액세스](../active-directory-conditional-access.md) 기능을 사용하여 사용자 계정을 보호할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="860d1-119">사용자가 비즈니스용 Skype 2016을 포함한 비즈니스용 Skype 클라이언트 응용 프로그램에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="860d1-120">사용자가 PowerShell v1.0에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="860d1-121">PowerShell v2.0을 대신 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="860d1-122">지원되지 않는 시나리오에 대한 해결 방법으로, Azure AD Connect 마법사의 [선택적 기능](active-directory-aadconnect-get-started-custom.md#optional-features) 페이지에서 암호 해시 동기화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span> <span data-ttu-id="860d1-123">암호 해시 동기화는 _단지_ 앞의 시나리오에 대한 대체 방법일 뿐이며 통과 인증에 대한 일반적인 대체 방법은 _아닙니다_.</span><span class="sxs-lookup"><span data-stu-id="860d1-123">Password Hash Synchronization acts as a fallback for the preceding scenarios _only_ (and _not_ as a generic fallback to Pass-through Authentication).</span></span> <span data-ttu-id="860d1-124">이러한 시나리오가 필요하지 않으면 암호 해시 동기화를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="860d1-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="860d1-125">Next steps</span></span>
- <span data-ttu-id="860d1-126">[**빠른 시작**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Azure AD 통과 인증을 작동하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="860d1-127">[**기술 심층 분석**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="860d1-128">[**FAQ(질문과 대답)**](active-directory-aadconnect-pass-through-authentication-faq.md) - 질문과 대답을 다루고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="860d1-129">[**문제 해결**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 기능과 관련된 일반적인 문제를 해결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="860d1-130">[**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="860d1-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="860d1-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
