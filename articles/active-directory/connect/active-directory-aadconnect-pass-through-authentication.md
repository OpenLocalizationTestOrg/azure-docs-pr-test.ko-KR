---
title: "Azure AD Connect: 통과 인증 | Microsoft 문서"
description: "이 문서에서는 Azure AD(Azure Active Directory) 통과 인증 및 이 통과 인증을 통해 사용자의 암호를 온-프레미스 Active Directory에 대해 유효성 검사하여 Azure AD 로그인을 허용하는 방법을 설명합니다."
services: active-directory
keywords: "Azure AD Connect 통과 인증의 정의, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 6acbc347d7b187a6aac603dd05cf95c6aba54475
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="3f2cd-104">Azure Active Directory 통과 인증으로 사용자 로그인</span><span class="sxs-lookup"><span data-stu-id="3f2cd-104">User sign-in with Azure Active Directory Pass-through Authentication</span></span>

## <a name="what-is-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="3f2cd-105">Azure Active Directory 통과 인증이란?</span><span class="sxs-lookup"><span data-stu-id="3f2cd-105">What is Azure Active Directory Pass-through Authentication?</span></span>

<span data-ttu-id="3f2cd-106">Azure AD(Azure Active Directory) 통과 인증을 사용하면 사용자가 온-프레미스와 클라우드 기반 응용 프로그램 둘 다에서 동일한 암호로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-106">Azure Active Directory (Azure AD) Pass-through Authentication allows your users to sign in to both on-premises and cloud-based applications using the same passwords.</span></span> <span data-ttu-id="3f2cd-107">이 기능은 하나 적은 기억할 암호로 사용자에게 더 나은 환경을 제공하고 사용자는 로그인하는 방법을 잊을 가능성이 적기 때문에 IT 기술 지원팀 비용을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-107">This feature provides your users a better experience - one less password to remember, and reduces IT helpdesk costs because your users are less likely to forget how to sign in.</span></span> <span data-ttu-id="3f2cd-108">사용자가 Azure AD를 사용하여 로그인할 때 이 기능은 온-프레미스 Active Directory에 대해 직접 사용자 암호의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-108">When users sign in using Azure AD, this feature validates users' passwords directly against your on-premises Active Directory.</span></span>

<span data-ttu-id="3f2cd-109">이 기능은 조직에 클라우드 인증과 동일한 혜택을 제공하는 [Azure AD 암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)에 대한 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-109">This feature is an alternative to [Azure AD Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md), which provides the same benefit of cloud authentication to organizations.</span></span> <span data-ttu-id="3f2cd-110">하지만 특정 조직에서 보안 및 규정 준수 정책은 이러한 조직이 내부 경계 외부의 해시된 폼에서도 사용자의 암호를 보내는 것을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-110">However, security and compliance policies in certain organizations don't permit these organizations to send users' passwords, even in a hashed form, outside their internal boundaries.</span></span> <span data-ttu-id="3f2cd-111">통과 인증은 이러한 조직에 적합한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-111">Pass-through Authentication is the right solution for such organizations.</span></span>

![Azure AD 통과 인증](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

<span data-ttu-id="3f2cd-113">통과 인증을 [Seamless Single Sign-On](active-directory-aadconnect-sso.md) 기능에 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-113">You can combine Pass-through Authentication with the [Seamless Single Sign-On](active-directory-aadconnect-sso.md) feature.</span></span> <span data-ttu-id="3f2cd-114">이러한 방식으로 사용자가 회사 네트워크 내부에서 회사 컴퓨터의 응용 프로그램에 액세스할 때 로그인하기 위해 암호를 입력할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-114">This way, when your users are accessing applications on their corporate machines inside your corporate network, they don't need to type in their passwords to sign in.</span></span>

>[!IMPORTANT]
><span data-ttu-id="3f2cd-115">Azure AD 통과 인증은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-115">Azure AD Pass-through Authentication is currently in preview.</span></span>

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a><span data-ttu-id="3f2cd-116">Azure AD 통과 인증 사용의 주요 혜택</span><span class="sxs-lookup"><span data-stu-id="3f2cd-116">Key benefits of using Azure AD Pass-through Authentication</span></span>

- <span data-ttu-id="3f2cd-117">*멋진 사용자 환경*</span><span class="sxs-lookup"><span data-stu-id="3f2cd-117">*Great user experience*</span></span>
  - <span data-ttu-id="3f2cd-118">사용자는 온-프레미스와 클라우드 기반 응용 프로그램에 로그인하는 데 동일한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-118">Users use the same passwords to sign into both on-premises and cloud-based applications.</span></span>
  - <span data-ttu-id="3f2cd-119">사용자는 암호 관련 문제를 해결하기 위해 IT 기술 지원팀과 소통하는 데 더 적은 시간을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-119">Users spend less time talking to the IT helpdesk resolving password-related issues.</span></span>
  - <span data-ttu-id="3f2cd-120">사용자는 클라우드에서 [셀프 서비스 암호 관리](../active-directory-passwords-overview.md) 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-120">Users can complete [self-service password management](../active-directory-passwords-overview.md) tasks in the cloud.</span></span>
- <span data-ttu-id="3f2cd-121">*손쉬운 배포 및 관리*</span><span class="sxs-lookup"><span data-stu-id="3f2cd-121">*Easy to deploy & administer*</span></span>
  - <span data-ttu-id="3f2cd-122">복잡한 온-프레미스 배포 또는 네트워크 구성에 대한 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-122">No need for complex on-premises deployments or network configuration.</span></span>
  - <span data-ttu-id="3f2cd-123">온-프레미스에 설치되는 간단한 에이전트만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-123">Needs just a lightweight agent to be installed on-premises.</span></span>
  - <span data-ttu-id="3f2cd-124">관리 오버헤드 없음</span><span class="sxs-lookup"><span data-stu-id="3f2cd-124">No management overhead.</span></span> <span data-ttu-id="3f2cd-125">에이전트는 향상된 기능 및 버그 수정을 자동으로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-125">The agent automatically receives improvements and bug fixes.</span></span>
- <span data-ttu-id="3f2cd-126">*보안*</span><span class="sxs-lookup"><span data-stu-id="3f2cd-126">*Secure*</span></span>
  - <span data-ttu-id="3f2cd-127">온-프레미스 암호가 어떤 형태로든 클라우드에 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-127">On-premises passwords are never stored in the cloud in any form.</span></span>
  - <span data-ttu-id="3f2cd-128">에이전트는 네트워크 내에서만 아웃바운드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-128">The agent only makes outbound connections from within your network.</span></span> <span data-ttu-id="3f2cd-129">따라서 DMZ라고도 하는 경계 네트워크에 에이전트를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-129">Therefore, there is no requirement to install the agent in a perimeter network, also known as a DMZ.</span></span>
  - <span data-ttu-id="3f2cd-130">MFA(Multi-Factor Authentication)를 포함하여 [Azure AD 조건부 액세스 정책](../active-directory-conditional-access-azure-portal.md)을 사용하여 원활하게 작동하고, [무차별 암호 대입 공격을 필터링](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)하여 사용자 계정을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-130">Protects your user accounts by working seamlessly with [Azure AD Conditional Access policies](../active-directory-conditional-access-azure-portal.md), including Multi-Factor Authentication (MFA), and by [filtering out brute force password attacks](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).</span></span>
- <span data-ttu-id="3f2cd-131">*고가용성*</span><span class="sxs-lookup"><span data-stu-id="3f2cd-131">*Highly available*</span></span>
  - <span data-ttu-id="3f2cd-132">로그인 요청의 고가용성을 제공하기 위해 여러 온-프레미스 서버에 에이전트를 추가로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-132">Additional agents can be installed on multiple on-premises servers to provide high availability of sign-in requests.</span></span>

## <a name="feature-highlights"></a><span data-ttu-id="3f2cd-133">주요 기능</span><span class="sxs-lookup"><span data-stu-id="3f2cd-133">Feature highlights</span></span>

- <span data-ttu-id="3f2cd-134">모든 웹 브라우저 기반 응용 프로그램 및 [최신 인증](https://aka.ms/modernauthga)을 사용하는 Microsoft Office 클라이언트 응용 프로그램에 사용자 로그인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-134">Supports user sign-in into all web browser-based applications and into Microsoft Office client applications that use [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="3f2cd-135">로그인 사용자 이름은 온-프레미스 기본 사용자 이름(`userPrincipalName`) 또는 Azure AD Connect에 구성된 다른 특성(`Alternate ID`라고 함) 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-135">Sign-in usernames can be either the on-premises default username (`userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
- <span data-ttu-id="3f2cd-136">기능은 MFA(Multi-Factor Authentication)와 같은 [조건부 액세스](../active-directory-conditional-access.md)를 사용하여 원활하게 작동하여 사용자를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-136">The feature works seamlessly with [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA) to help secure your users.</span></span>
- <span data-ttu-id="3f2cd-137">AD 포리스트 간에 포리스트 트러스트가 있고 이름 접미사 라우팅이 제대로 구성된 경우 다중 포리스트 환경이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-137">Multi-forest environments are supported if there are forest trusts between your AD forests and if name suffix routing is correctly configured.</span></span>
- <span data-ttu-id="3f2cd-138">무료 기능이며 이 기능을 사용하는 데는 Azure AD 유료 버전이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-138">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span>
- <span data-ttu-id="3f2cd-139">[Azure AD Connect](active-directory-aadconnect.md)를 통해 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-139">It can be enabled via [Azure AD Connect](active-directory-aadconnect.md).</span></span>
- <span data-ttu-id="3f2cd-140">암호 유효성 검사 요청을 수신하고 이에 응답하는 간단한 온-프레미스 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-140">It uses a lightweight on-premises agent that listens for and responds to password validation requests.</span></span>
- <span data-ttu-id="3f2cd-141">여러 에이전트를 설치하면 로그인 요청의 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-141">Installing multiple agents provides high availability of sign-in requests.</span></span>
- <span data-ttu-id="3f2cd-142">이렇게 하면 클라우드의 무차별 암호 대입 공격으로부터 온-프레미스 계정이 [보호](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-142">It [protects](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) your on-premises accounts against brute force password attacks in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f2cd-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f2cd-143">Next steps</span></span>

- <span data-ttu-id="3f2cd-144">[**빠른 시작**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Azure AD 통과 인증을 작동하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-144">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="3f2cd-145">[**현재 제한 사항**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 이 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-145">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="3f2cd-146">지원되는 시나리오와 지원되지 않는 시나리오를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-146">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="3f2cd-147">[**기술 심층 분석**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-147">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="3f2cd-148">[**FAQ(질문과 대답)**](active-directory-aadconnect-pass-through-authentication-faq.md) - 질문과 대답을 다루고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-148">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="3f2cd-149">[**문제 해결**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 기능과 관련된 일반적인 문제를 해결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-149">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="3f2cd-150">[**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-150">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="3f2cd-151">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="3f2cd-151">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
