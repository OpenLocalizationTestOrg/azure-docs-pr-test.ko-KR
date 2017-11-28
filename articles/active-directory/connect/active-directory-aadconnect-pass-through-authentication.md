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
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="b02d4-104">Azure Active Directory 통과 인증으로 사용자 로그인</span><span class="sxs-lookup"><span data-stu-id="b02d4-104">User sign-in with Azure Active Directory Pass-through Authentication</span></span>

## <a name="what-is-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="b02d4-105">Azure Active Directory 통과 인증이란?</span><span class="sxs-lookup"><span data-stu-id="b02d4-105">What is Azure Active Directory Pass-through Authentication?</span></span>

<span data-ttu-id="b02d4-106">Azure Active Directory (Azure AD) 통과 인증 사용자 toosign tooboth 온-프레미스에 있으며이 사용 하 여 클라우드 기반 응용 프로그램에 동일한 암호 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-106">Azure Active Directory (Azure AD) Pass-through Authentication allows your users toosign in tooboth on-premises and cloud-based applications using hello same passwords.</span></span> <span data-ttu-id="b02d4-107">이 기능은 사용자가 더 나은 환경을-적은 암호 tooremember 하나를 제공 하 고 사용자가 거의 tooforget 어떻게 하기 때문에 IT 기술 지원팀 비용 감소에 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-107">This feature provides your users a better experience - one less password tooremember, and reduces IT helpdesk costs because your users are less likely tooforget how toosign in.</span></span> <span data-ttu-id="b02d4-108">사용자가 Azure AD를 사용하여 로그인할 때 이 기능은 온-프레미스 Active Directory에 대해 직접 사용자 암호의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-108">When users sign in using Azure AD, this feature validates users' passwords directly against your on-premises Active Directory.</span></span>

<span data-ttu-id="b02d4-109">이 기능은 대신 너무[Azure AD 암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)를 제공 하는 클라우드 인증 tooorganizations의 동일한 이점은 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-109">This feature is an alternative too[Azure AD Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md), which provides hello same benefit of cloud authentication tooorganizations.</span></span> <span data-ttu-id="b02d4-110">하지만, 특정 조직에서 보안 및 규정 준수 정책을 하지 허용 이러한 조직 toosend 사용자의 암호는 해시 된 폼 내부 경계가 외부에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-110">However, security and compliance policies in certain organizations don't permit these organizations toosend users' passwords, even in a hashed form, outside their internal boundaries.</span></span> <span data-ttu-id="b02d4-111">통과 인증은 그러한 조직의 hello 적합 한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-111">Pass-through Authentication is hello right solution for such organizations.</span></span>

![Azure AD 통과 인증](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

<span data-ttu-id="b02d4-113">통과 인증 hello로 결합할 수 있습니다 [원활한 Single Sign-on](active-directory-aadconnect-sso.md) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-113">You can combine Pass-through Authentication with hello [Seamless Single Sign-On](active-directory-aadconnect-sso.md) feature.</span></span> <span data-ttu-id="b02d4-114">이러한 방식으로 사용자가 회사 컴퓨터 사용자가 회사 네트워크 내부에서 응용 프로그램에 액세스 하는 경우, 이러한 tootype에 자신의 암호 toosign에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-114">This way, when your users are accessing applications on their corporate machines inside your corporate network, they don't need tootype in their passwords toosign in.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b02d4-115">Azure AD 통과 인증은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-115">Azure AD Pass-through Authentication is currently in preview.</span></span>

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a><span data-ttu-id="b02d4-116">Azure AD 통과 인증 사용의 주요 혜택</span><span class="sxs-lookup"><span data-stu-id="b02d4-116">Key benefits of using Azure AD Pass-through Authentication</span></span>

- <span data-ttu-id="b02d4-117">*멋진 사용자 환경*</span><span class="sxs-lookup"><span data-stu-id="b02d4-117">*Great user experience*</span></span>
  - <span data-ttu-id="b02d4-118">Hello를 사용 하는 사용자가 온-프레미스 및 클라우드 기반 응용 프로그램 모두에 동일한 암호 toosign 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-118">Users use hello same passwords toosign into both on-premises and cloud-based applications.</span></span>
  - <span data-ttu-id="b02d4-119">사용자가 시간이 절약 toohello 통하게 IT 기술 지원팀 암호 관련 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-119">Users spend less time talking toohello IT helpdesk resolving password-related issues.</span></span>
  - <span data-ttu-id="b02d4-120">사용자가 צ ְ ײ [셀프 서비스 암호 관리](../active-directory-passwords-overview.md) hello 클라우드에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-120">Users can complete [self-service password management](../active-directory-passwords-overview.md) tasks in hello cloud.</span></span>
- <span data-ttu-id="b02d4-121">*쉬운 toodeploy & 관리*</span><span class="sxs-lookup"><span data-stu-id="b02d4-121">*Easy toodeploy & administer*</span></span>
  - <span data-ttu-id="b02d4-122">복잡한 온-프레미스 배포 또는 네트워크 구성에 대한 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-122">No need for complex on-premises deployments or network configuration.</span></span>
  - <span data-ttu-id="b02d4-123">필요한 경량 에이전트 toobe 방금 온-프레미스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-123">Needs just a lightweight agent toobe installed on-premises.</span></span>
  - <span data-ttu-id="b02d4-124">관리 오버헤드 없음</span><span class="sxs-lookup"><span data-stu-id="b02d4-124">No management overhead.</span></span> <span data-ttu-id="b02d4-125">hello 에이전트 향상 및 버그 수정에 자동으로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-125">hello agent automatically receives improvements and bug fixes.</span></span>
- <span data-ttu-id="b02d4-126">*보안*</span><span class="sxs-lookup"><span data-stu-id="b02d4-126">*Secure*</span></span>
  - <span data-ttu-id="b02d4-127">모든 형태의 hello 클라우드에서 온-프레미스 암호 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-127">On-premises passwords are never stored in hello cloud in any form.</span></span>
  - <span data-ttu-id="b02d4-128">hello 에이전트만 네트워크 내에서 아웃 바운드 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-128">hello agent only makes outbound connections from within your network.</span></span> <span data-ttu-id="b02d4-129">따라서 DMZ 라고도 하는 경계 네트워크에서는 요구 사항 tooinstall hello 에이전트가 없습니다.이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-129">Therefore, there is no requirement tooinstall hello agent in a perimeter network, also known as a DMZ.</span></span>
  - <span data-ttu-id="b02d4-130">MFA(Multi-Factor Authentication)를 포함하여 [Azure AD 조건부 액세스 정책](../active-directory-conditional-access-azure-portal.md)을 사용하여 원활하게 작동하고, [무차별 암호 대입 공격을 필터링](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)하여 사용자 계정을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-130">Protects your user accounts by working seamlessly with [Azure AD Conditional Access policies](../active-directory-conditional-access-azure-portal.md), including Multi-Factor Authentication (MFA), and by [filtering out brute force password attacks](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).</span></span>
- <span data-ttu-id="b02d4-131">*고가용성*</span><span class="sxs-lookup"><span data-stu-id="b02d4-131">*Highly available*</span></span>
  - <span data-ttu-id="b02d4-132">여러 온-프레미스 서버 tooprovide 고가용성 로그인 요청에 추가 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-132">Additional agents can be installed on multiple on-premises servers tooprovide high availability of sign-in requests.</span></span>

## <a name="feature-highlights"></a><span data-ttu-id="b02d4-133">주요 기능</span><span class="sxs-lookup"><span data-stu-id="b02d4-133">Feature highlights</span></span>

- <span data-ttu-id="b02d4-134">모든 웹 브라우저 기반 응용 프로그램 및 [최신 인증](https://aka.ms/modernauthga)을 사용하는 Microsoft Office 클라이언트 응용 프로그램에 사용자 로그인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-134">Supports user sign-in into all web browser-based applications and into Microsoft Office client applications that use [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="b02d4-135">사용자 로그인 이름 hello 온-프레미스 기본 사용자 이름 중 하나가 될 수 있습니다 (`userPrincipalName`) 또는 Azure AD Connect에서 구성 하는 다른 특성 (라고 `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="b02d4-135">Sign-in usernames can be either hello on-premises default username (`userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
- <span data-ttu-id="b02d4-136">hello 기능으로 원활 하 게 작동 [조건부 액세스](../active-directory-conditional-access.md) Multi-factor Authentication (MFA) toohelp 등의 기능 사용자가 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-136">hello feature works seamlessly with [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA) toohelp secure your users.</span></span>
- <span data-ttu-id="b02d4-137">AD 포리스트 간에 포리스트 트러스트가 있고 이름 접미사 라우팅이 제대로 구성된 경우 다중 포리스트 환경이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-137">Multi-forest environments are supported if there are forest trusts between your AD forests and if name suffix routing is correctly configured.</span></span>
- <span data-ttu-id="b02d4-138">사용 가능한 기능 및 모든 유료 버전의 Azure AD toouse 필요 하지 않습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-138">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span>
- <span data-ttu-id="b02d4-139">[Azure AD Connect](active-directory-aadconnect.md)를 통해 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-139">It can be enabled via [Azure AD Connect](active-directory-aadconnect.md).</span></span>
- <span data-ttu-id="b02d4-140">수신 대기 하 고 toopassword 유효성 검사 요청에 응답 하는 간단한 온-프레미스 에이전트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-140">It uses a lightweight on-premises agent that listens for and responds toopassword validation requests.</span></span>
- <span data-ttu-id="b02d4-141">여러 에이전트를 설치하면 로그인 요청의 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-141">Installing multiple agents provides high availability of sign-in requests.</span></span>
- <span data-ttu-id="b02d4-142">그 [보호](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) 무차별 암호에 대 한 온-프레미스 계정 hello 클라우드에서 무차별 암호 대입 공격을 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-142">It [protects](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) your on-premises accounts against brute force password attacks in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b02d4-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b02d4-143">Next steps</span></span>

- <span data-ttu-id="b02d4-144">[**빠른 시작**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Azure AD 통과 인증을 작동하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-144">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="b02d4-145">[**현재 제한 사항**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 이 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-145">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="b02d4-146">지원되는 시나리오와 지원되지 않는 시나리오를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-146">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="b02d4-147">[**기술 심층 분석**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-147">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="b02d4-148">[**질문과 대답** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 질문과 대답을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-148">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="b02d4-149">[**문제를 해결** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-149">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="b02d4-150">[**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-150">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="b02d4-151">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="b02d4-151">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
