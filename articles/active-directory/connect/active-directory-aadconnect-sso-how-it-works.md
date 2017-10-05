---
title: "Azure AD Connect: Seamless Single Sign-On - 작동 방식 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory Seamless Single Sign-On 기능이 작동하는 방식을 설명합니다."
services: active-directory
keywords: "Azure AD Connect의 정의, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: f0bcbdb03fbb70ff91ac3a56974a88eb1b26c245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="8b4e0-104">Azure Active Directory Seamless Single Sign-On: 기술 심층 분석</span><span class="sxs-lookup"><span data-stu-id="8b4e0-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="8b4e0-105">이 문서에서는 Azure Active Directory Seamless SSO(Seamless Single Sign-On) 기능이 어떻게 작동하는지에 대한 기술적인 정보에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8b4e0-106">Seamless SSO 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-106">The Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="8b4e0-107">Seamless SSO 작동 방식</span><span class="sxs-lookup"><span data-stu-id="8b4e0-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="8b4e0-108">이 섹션은 두 부분으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-108">This section has two parts to it:</span></span>
1. <span data-ttu-id="8b4e0-109">Seamless SSO 기능 설정</span><span class="sxs-lookup"><span data-stu-id="8b4e0-109">The setup of the Seamless SSO feature.</span></span>
2. <span data-ttu-id="8b4e0-110">단일 사용자 로그인 트랜잭션이 Seamless SSO와 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="8b4e0-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="8b4e0-111">기능을 설정하는 방식</span><span class="sxs-lookup"><span data-stu-id="8b4e0-111">How does set up work?</span></span>

<span data-ttu-id="8b4e0-112">Seamless SSO는 [여기](active-directory-aadconnect-sso-quick-start.md)서 보여 주듯이 Azure AD Connect를 통해 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="8b4e0-113">이 기능을 사용하도록 설정하는 동안 발생하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-113">While enabling the feature, the following steps occur:</span></span>
- <span data-ttu-id="8b4e0-114">온-프레미스 AD(Active Directory)에 Azure AD를 나타내는`AZUREADSSOACCT`라는 컴퓨터 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="8b4e0-115">컴퓨터 계정의 Kerberos 암호 해독 키가 Azure AD와 안전하게 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="8b4e0-116">또한 Azure AD 로그인 중에 사용되는 두 개의 URL을 나타내기 위해 두 개의 Kerberos SPN(서비스 사용자 이름)도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-116">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="8b4e0-117">컴퓨터 계정과 Kerberos SPN은 Azure AD Connect를 통해 Azure AD와 동기화하는 각 AD 포리스트에서, 그리고 Seamless SSO의 대상이 되는 사용자에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-117">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="8b4e0-118">다른 컴퓨터 계정이 저장된 OU(조직 단위)로 `AZUREADSSOACCT` 컴퓨터 계정을 이동하여 동일한 방식으로 관리되고 삭제되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-118">Move the `AZUREADSSOACCT` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8b4e0-119">적어도 30일마다 `AZUREADSSOACCT` 컴퓨터 계정의 [Kerberos 암호 해독 키를 롤오버](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account)하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-119">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of the `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="8b4e0-120">Seamless SSO로 로그인하는 방식</span><span class="sxs-lookup"><span data-stu-id="8b4e0-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="8b4e0-121">설정이 완료되면 Seamless SSO는 IWA(Windows 통합 인증)를 사용하는 다른 로그인과 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="8b4e0-122">흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-122">The flow is as follows:</span></span>

1. <span data-ttu-id="8b4e0-123">사용자가 회사 네트워크의 도메인 가입 회사 장치에서 응용 프로그램(예: Outlook Web App - https://outlook.office365.com/owa/)에 액세스하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-123">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="8b4e0-124">사용자가 아직 로그인하지 않은 경우 해당 사용자는 Azure AD 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-124">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="8b4e0-125">Azure AD 로그인 요청에 `domain_hint`(테넌트(예: contoso.onmicrosoft.com) 식별) 또는 `login_hint`(사용자(예: user@contoso.onmicrosoft.com 또는 user@contoso.com) 식별) 매개 변수가 포함된 경우 2단계는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-125">If the Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying the user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="8b4e0-126">사용자는 자신의 사용자 이름을 Azure AD 로그인 페이지에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-126">The user types in their user name into the Azure AD sign-in page.</span></span>
4. <span data-ttu-id="8b4e0-127">Azure AD는 백그라운드에서 JavaScript를 사용하여 401 권한 없음 응답을 통해 브라우저에 Kerberos 티켓을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-127">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span></span>
5. <span data-ttu-id="8b4e0-128">그런 다음 브라우저는 Active Directory에서 Azure AD를 나타내는 `AZUREADSSOACCT` 컴퓨터 계정에 대한 티켓을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-128">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="8b4e0-129">Active Directory는 컴퓨터 계정을 찾아서 컴퓨터 계정의 비밀로 암호화된 Kerberos 티켓을 브라우저에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-129">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span></span>
7. <span data-ttu-id="8b4e0-130">브라우저는 Active Directory에서 가져온 Kerberos 티켓을 Azure AD([이전에 브라우저의 인트라넷 영역 설정에 추가된 Azure AD URL](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature) 중 하나에 있음)로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-130">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD (on one of the [Azure AD URLs previously added to the browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="8b4e0-131">Azure AD는 이전에 공유한 키를 사용하여 회사 장치에 로그인한 사용자의 ID가 포함된 Kerberos 티켓을 암호 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-131">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span></span>
9. <span data-ttu-id="8b4e0-132">평가 후에 Azure AD는 응용 프로그램에 토큰을 반환하거나 사용자에게 Multi-Factor Authentication과 같은 추가 증명을 수행하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-132">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="8b4e0-133">사용자 로그인에 성공하면 해당 사용자는 해당 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-133">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="8b4e0-134">다음 다이어그램은 관련된 모든 구성 요소와 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-134">The following diagram illustrates all the components and the steps involved.</span></span>

![Seamless Single Sign-On](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="8b4e0-136">Seamless SSO는 편의적인 기능입니다. 이는 SSO가 실패하면 로그인 환경은 일반 동작으로 돌아감을 의미합니다. 즉 사용자가 자신의 암호를 입력하여 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-136">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b4e0-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b4e0-137">Next steps</span></span>

- <span data-ttu-id="8b4e0-138">[**빠른 시작**](active-directory-aadconnect-sso-quick-start.md) - Azure AD Seamless SSO를 준비하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="8b4e0-139">[**FAQ(질문과 대답)**](active-directory-aadconnect-sso-faq.md) - 질문과 대답을 다루고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="8b4e0-140">[**문제 해결**](active-directory-aadconnect-troubleshoot-sso.md) - 기능과 관련된 일반적인 문제를 해결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="8b4e0-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="8b4e0-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
