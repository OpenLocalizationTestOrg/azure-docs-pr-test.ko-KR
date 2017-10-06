---
title: "Azure AD Connect: 통과 인증 - 작동 방식? | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory 통과 인증 작동 방식을 설명합니다."
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
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="e8c99-105">Azure Active Directory 통과 인증: 기술 심층 분석</span><span class="sxs-lookup"><span data-stu-id="e8c99-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="e8c99-106">Azure AD 통과 인증은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="e8c99-107">Azure Active Directory 통과 인증 작동 방식은?</span><span class="sxs-lookup"><span data-stu-id="e8c99-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="e8c99-108">사용자는 Azure Active Directory (Azure AD)에 의해 보호 되는 응용 프로그램에 toosign를 시도 하 고 hello hello 테 넌 트에서 통과 인증을 사용 하는 경우 다음 단계가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="e8c99-109">hello 사용자가 tooaccess 응용 프로그램 (예를 들어 Outlook Web App-hello https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="e8c99-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="e8c99-110">Hello 사용자 서명 되지 않은 경우 hello 사용자가 Azure AD 로그인 페이지로 리디렉션된 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="e8c99-111">hello 사용자 hello Azure AD 로그인 페이지에 자신의 사용자 이름과 암호를 입력 하 고 hello "로그인" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="e8c99-112">Hello 로그인 요청을 수신한 경우에 azure AD hello 사용자 이름 및 암호 (공개 키를 사용 하 여 암호화) 큐에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="e8c99-113">온-프레미스 통과 인증 에이전트 아웃 바운드 호출 toohello 큐를 만들고 hello 사용자 이름 및 암호화 된 암호를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="e8c99-114">hello 에이전트는 해당 개인 키를 사용 하 여 hello 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="e8c99-115">다음 hello 에이전트 hello 사용자 이름 및 암호 (유사한 메커니즘 toowhat Active Directory Federation Services에서 사용 됨)는 표준 Windows Api를 사용 하 여 Active Directory에 대해 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="e8c99-116">hello username 수 hello 온-프레미스 기본 사용자 이름 중 하나 (일반적으로 `userPrincipalName`) 또는 Azure AD Connect에서 구성 하는 다른 특성 (라고 `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="e8c99-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="e8c99-117">hello 온-프레미스 Active Directory 도메인 컨트롤러 (DC) 다음 hello 요청을 평가 하 고 반환 hello 적절 한 응답 (성공, 실패, 암호 만료 되었거나 사용자 차단) toohello 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="e8c99-118">hello 에이전트 차례로이 응답 백 tooAzure AD를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="e8c99-119">Azure AD는 hello 응답을 평가 하 고 적절 하 게 toohello 사용자 응답-예를 들어 hello 사용자가 즉시 로그인 하거나 Multi-factor Authentication (MFA)에 대 한 요청.</span><span class="sxs-lookup"><span data-stu-id="e8c99-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="e8c99-120">Hello 사용자 로그인에 성공한 경우 hello 사용자는 수 tooaccess hello 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="e8c99-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="e8c99-121">hello 다음 다이어그램에서는 모든 hello 구성 요소와 관련 된 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![통과 인증](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="e8c99-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8c99-123">Next steps</span></span>
- <span data-ttu-id="e8c99-124">[**현재 제한 사항**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 이 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="e8c99-125">지원되는 시나리오와 지원되지 않는 시나리오를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="e8c99-126">[**빠른 시작**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Azure AD 통과 인증을 작동하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="e8c99-127">[**질문과 대답** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 질문과 대답을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="e8c99-128">[**문제를 해결** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="e8c99-129">[**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="e8c99-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c99-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
