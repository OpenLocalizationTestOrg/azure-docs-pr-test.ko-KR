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
ms.openlocfilehash: d34ccd40082edbe036d963ad548bff648119bdd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="c1758-105">Azure Active Directory 통과 인증: 기술 심층 분석</span><span class="sxs-lookup"><span data-stu-id="c1758-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="c1758-106">Azure AD 통과 인증은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="c1758-107">Azure Active Directory 통과 인증 작동 방식은?</span><span class="sxs-lookup"><span data-stu-id="c1758-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="c1758-108">사용자가 Azure AD(Azure Active Directory)로 보호되는 응용 프로그램에 로그인하려고 하고 통과 인증이 테넌트에서 사용하도록 설정되어 있으면 다음 단계가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-108">When a user attempts to sign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on the tenant, the following steps occur:</span></span>

1. <span data-ttu-id="c1758-109">사용자가 응용 프로그램에 액세스하려고 합니다(예: Outlook 웹앱 - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="c1758-109">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="c1758-110">사용자가 아직 로그인하지 않은 경우 해당 사용자는 Azure AD 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-110">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>
3. <span data-ttu-id="c1758-111">사용자가 사용자 이름과 암호를 Azure AD 로그인 페이지에 입력하고 "로그인" 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-111">The user enters their username and password into the Azure AD sign-in page and clicks the "Sign in" button.</span></span>
4. <span data-ttu-id="c1758-112">로그인 요청을 수신하는 Azure AD에서 공개 키로 암호화된 사용자 이름 및 암호를 큐에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-112">Azure AD, on receiving the sign-in request, places the username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="c1758-113">온-프레미스 통과 인증 에이전트는 큐에 아웃바운드 호출을 실행하고 사용자 이름 및 암호화된 암호를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-113">An on-premises Pass-through Authentication agent makes an outbound call to the queue and retrieves the username and encrypted password.</span></span>
6. <span data-ttu-id="c1758-114">에이전트는 해당 개인 키를 사용하여 암호를 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-114">The agent decrypts the password using its private key.</span></span>
7. <span data-ttu-id="c1758-115">그런 다음 에이전트가 표준 Windows API(Active Directory Federation Services에서 사용되는 것과 비슷한 메커니즘)를 사용하여 사용자 이름과 암호를 Active Directory에 대해 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-115">The agent then validates the username and password against Active Directory using standard Windows APIs (a similar mechanism to what is used by Active Directory Federation Services).</span></span> <span data-ttu-id="c1758-116">사용자 이름은 온-프레미스 기본 사용자 이름(일반적으로 `userPrincipalName`) 또는 Azure AD Connect에 구성된 또 다른 특성(`Alternate ID`라고 함) 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-116">The username can be either the on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="c1758-117">그런 다음 온-프레미스 Active Directory DC(도메인 컨트롤러)는 요청을 평가하고 적절한 응답(성공, 실패, 암호 만료됨 또는 사용자 차단됨)을 에이전트에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-117">The on-premises Active Directory Domain Controller (DC) then evaluates the request and returns the appropriate response (success, failure, password expired or user locked out) to the agent.</span></span>
9. <span data-ttu-id="c1758-118">그러면 에이전트가 이 응답을 다시 Azure AD로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-118">The agent, in turn, returns this response back to Azure AD.</span></span>
10. <span data-ttu-id="c1758-119">Azure AD는 응답을 평가하고 사용자에게 적절히 응답합니다(예: 사용자가 즉시 로그인하도록 하거나 MFA(Multi-Factor Authentication)에 대해 요청).</span><span class="sxs-lookup"><span data-stu-id="c1758-119">Azure AD evaluates the response and responds to the user as appropriate - for example, it either signs the user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="c1758-120">사용자 로그인에 성공하면 해당 사용자는 해당 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-120">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="c1758-121">다음 다이어그램은 관련된 모든 구성 요소와 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-121">The following diagram illustrates all the components and the steps involved.</span></span>

![통과 인증](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="c1758-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1758-123">Next steps</span></span>
- <span data-ttu-id="c1758-124">[**현재 제한 사항**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 이 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="c1758-125">지원되는 시나리오와 지원되지 않는 시나리오를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="c1758-126">[**빠른 시작**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Azure AD 통과 인증을 작동하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="c1758-127">[**FAQ(질문과 대답)**](active-directory-aadconnect-pass-through-authentication-faq.md) - 질문과 대답을 다루고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="c1758-128">[**문제 해결**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 기능과 관련된 일반적인 문제를 해결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="c1758-129">[**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="c1758-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="c1758-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
