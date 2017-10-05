---
title: "Azure MFA 클라우드 또는 서버 중에서 선택 | Microsoft Docs"
description: "보안을 유지하려는 대상과 사용자의 위치에 대한 질문에 답하여 적합한 다단계 인증 보안 솔루션을 선택합니다.  클라우드, MFA 서버 또는 AD FS를 선택합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 6f8ee3449244b12d2c8b5714e6ad893e2f0b10ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="choose-the-azure-multi-factor-authentication-solution-for-you"></a><span data-ttu-id="8dbb7-104">사용자를 위한 Azure Multi-Factor Authentication 솔루션 선택</span><span class="sxs-lookup"><span data-stu-id="8dbb7-104">Choose the Azure Multi-Factor Authentication solution for you</span></span>
<span data-ttu-id="8dbb7-105">Azure MFA(Multi-Factor Authentication)에는 여러 가지 버전이 있기 때문에 사용하기에 적절한 버전을 파악하기 위해 몇 가지 질문에 답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dbb7-105">Because there are several flavors of Azure Multi-Factor Authentication (MFA), we must answer a few questions to figure out which version is the proper one to use.</span></span>  <span data-ttu-id="8dbb7-106">해당 질문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbb7-106">Those questions are:</span></span>

* [<span data-ttu-id="8dbb7-107">보안을 유지하려는 대상은 무엇입니까</span><span class="sxs-lookup"><span data-stu-id="8dbb7-107">What am I trying to secure</span></span>](#what-am-i-trying-to-secure)
* [<span data-ttu-id="8dbb7-108">사용자는 어디에 있습니까</span><span class="sxs-lookup"><span data-stu-id="8dbb7-108">Where are the users located</span></span>](#where-are-the-users-located)
* [<span data-ttu-id="8dbb7-109">어떤 기능이 필요합니까?</span><span class="sxs-lookup"><span data-stu-id="8dbb7-109">What features do I need?</span></span>](#what-featured-do-i-need)

<span data-ttu-id="8dbb7-110">다음 섹션에서는 이러한 각 대답의 결정에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8dbb7-110">The following sections provide guidance on determining each of these answers.</span></span>

## <a name="what-am-i-trying-to-secure"></a><span data-ttu-id="8dbb7-111">보안을 유지하려는 대상은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8dbb7-111">What am I trying to secure?</span></span>
<span data-ttu-id="8dbb7-112">올바른 2단계 인증 솔루션을 결정하려면 먼저 두 번째 인증 방법으로 보안을 유지하려는 대상이 무엇인지 답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dbb7-112">To determine the correct two-step verification solution, first we must answer the question of what are you trying to secure with a second method of authentication.</span></span>  <span data-ttu-id="8dbb7-113">Azure에 있는 응용프로그램입니까?</span><span class="sxs-lookup"><span data-stu-id="8dbb7-113">Is it an application that is in Azure?</span></span>  <span data-ttu-id="8dbb7-114">또는 원격 액세스 시스템입니까?</span><span class="sxs-lookup"><span data-stu-id="8dbb7-114">Or a remote access system?</span></span>  <span data-ttu-id="8dbb7-115">보안을 유지하려는 대상이 무엇인지 결정하여 Multi-Factor Authentication 활성화가 필요한 곳에 대한 질문에 답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbb7-115">By determining what we are trying to secure, we can answer the question of where Multi-Factor Authentication needs to be enabled.</span></span>  

| <span data-ttu-id="8dbb7-116">보안을 유지하려는 대상은 무엇입니까</span><span class="sxs-lookup"><span data-stu-id="8dbb7-116">What are you trying to secure</span></span> | <span data-ttu-id="8dbb7-117">클라우드의 MFA</span><span class="sxs-lookup"><span data-stu-id="8dbb7-117">MFA in the cloud</span></span> | <span data-ttu-id="8dbb7-118">MFA 서버 </span><span class="sxs-lookup"><span data-stu-id="8dbb7-118">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="8dbb7-119">자사 Microsoft 앱</span><span class="sxs-lookup"><span data-stu-id="8dbb7-119">First-party Microsoft apps</span></span> |<span data-ttu-id="8dbb7-120">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-120">●</span></span> |<span data-ttu-id="8dbb7-121">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-121">●</span></span> |
| <span data-ttu-id="8dbb7-122">앱 갤러리의 SaaS 앱</span><span class="sxs-lookup"><span data-stu-id="8dbb7-122">SaaS apps in the app gallery</span></span> |<span data-ttu-id="8dbb7-123">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-123">●</span></span> |  |
| <span data-ttu-id="8dbb7-124">Azure AD 앱 프록시를 통해 웹 응용프로그램 게시됨</span><span class="sxs-lookup"><span data-stu-id="8dbb7-124">Web applications published through Azure AD App Proxy</span></span> |<span data-ttu-id="8dbb7-125">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-125">●</span></span> |  |
| <span data-ttu-id="8dbb7-126">Azure AD 응용프로그램 프록시를 통해 IIS 응용프로그램 게시되지 않음</span><span class="sxs-lookup"><span data-stu-id="8dbb7-126">IIS applications not published through Azure AD App Proxy</span></span> | |<span data-ttu-id="8dbb7-127">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-127">●</span></span> |
| <span data-ttu-id="8dbb7-128">VPN, RDG와 같은 원격 액세스</span><span class="sxs-lookup"><span data-stu-id="8dbb7-128">Remote access such as VPN, RDG</span></span> | <span data-ttu-id="8dbb7-129">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-129">●</span></span> | <span data-ttu-id="8dbb7-130">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-130">●</span></span> |

## <a name="where-are-the-users-located"></a><span data-ttu-id="8dbb7-131">사용자는 어디에 있습니까</span><span class="sxs-lookup"><span data-stu-id="8dbb7-131">Where are the users located</span></span>
<span data-ttu-id="8dbb7-132">다음으로 사용자의 위치를 확인하여 사용할 올바른 솔루션이 클라우드에 있는지 MFA 서버를 사용한 온-프레미스인지를 확인하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8dbb7-132">Next, looking at where our users are located helps to determine the correct solution to use, whether in the cloud or on-premises using the MFA Server.</span></span>

| <span data-ttu-id="8dbb7-133">사용자 위치</span><span class="sxs-lookup"><span data-stu-id="8dbb7-133">User Location</span></span> | <span data-ttu-id="8dbb7-134">클라우드의 MFA</span><span class="sxs-lookup"><span data-stu-id="8dbb7-134">MFA in the cloud</span></span> | <span data-ttu-id="8dbb7-135">MFA 서버 </span><span class="sxs-lookup"><span data-stu-id="8dbb7-135">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="8dbb7-136">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dbb7-136">Azure Active Directory</span></span> |<span data-ttu-id="8dbb7-137">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-137">●</span></span> | |
| <span data-ttu-id="8dbb7-138">Azure AD 및 AD FS로 페더레이션을 사용한 온-프레미스 AD</span><span class="sxs-lookup"><span data-stu-id="8dbb7-138">Azure AD and on-premises AD using federation with AD FS</span></span> |<span data-ttu-id="8dbb7-139">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-139">●</span></span> |<span data-ttu-id="8dbb7-140">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-140">●</span></span> |
| <span data-ttu-id="8dbb7-141">Azure AD 및 DirSync를 사용한 온-프레미스 AD, Azure AD Sync, Azure AD Connect - 암호 동기화 없음</span><span class="sxs-lookup"><span data-stu-id="8dbb7-141">Azure AD and on-premises AD using DirSync, Azure AD Sync, Azure AD Connect - no password sync</span></span> |<span data-ttu-id="8dbb7-142">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-142">●</span></span> |<span data-ttu-id="8dbb7-143">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-143">●</span></span> |
| <span data-ttu-id="8dbb7-144">Azure AD 및 DirSync를 사용한 온-프레미스 AD, Azure AD Sync, Azure AD Connect - 암호 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="8dbb7-144">Azure AD and on-premises AD using DirSync, Azure AD Sync, Azure AD Connect - with password sync</span></span> |<span data-ttu-id="8dbb7-145">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-145">●</span></span> | |
| <span data-ttu-id="8dbb7-146">온-프레미스 Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dbb7-146">On-premises Active Directory</span></span> | |<span data-ttu-id="8dbb7-147">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-147">●</span></span> |

## <a name="what-features-do-i-need"></a><span data-ttu-id="8dbb7-148">어떤 기능이 필요합니까?</span><span class="sxs-lookup"><span data-stu-id="8dbb7-148">What features do I need?</span></span>
<span data-ttu-id="8dbb7-149">다음 표는 클라우드에서 Multi-Factor Authentication과 함께 사용할 수 있는 경우와 Multi-Factor Authentication 서버와 함께 사용할 수 있는 경우에 대한 기능 비교입니다.</span><span class="sxs-lookup"><span data-stu-id="8dbb7-149">The following table compares the features that are available with Multi-Factor Authentication in the cloud and with the Multi-Factor Authentication Server.</span></span>

| <span data-ttu-id="8dbb7-150">기능</span><span class="sxs-lookup"><span data-stu-id="8dbb7-150">Feature</span></span> | <span data-ttu-id="8dbb7-151">클라우드의 MFA</span><span class="sxs-lookup"><span data-stu-id="8dbb7-151">MFA in the cloud</span></span> | <span data-ttu-id="8dbb7-152">MFA 서버 </span><span class="sxs-lookup"><span data-stu-id="8dbb7-152">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="8dbb7-153">두 번째 단계로 모바일 앱 알림</span><span class="sxs-lookup"><span data-stu-id="8dbb7-153">Mobile app notification as a second factor</span></span> | <span data-ttu-id="8dbb7-154">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-154">●</span></span> | <span data-ttu-id="8dbb7-155">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-155">●</span></span> |
| <span data-ttu-id="8dbb7-156">두 번째 단계로 모바일 앱 확인 코드</span><span class="sxs-lookup"><span data-stu-id="8dbb7-156">Mobile app verification code as a second factor</span></span> | <span data-ttu-id="8dbb7-157">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-157">●</span></span> | <span data-ttu-id="8dbb7-158">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-158">●</span></span> |
| <span data-ttu-id="8dbb7-159">두 번째 단계로 전화 통화</span><span class="sxs-lookup"><span data-stu-id="8dbb7-159">Phone call as second factor</span></span> | <span data-ttu-id="8dbb7-160">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-160">●</span></span> | <span data-ttu-id="8dbb7-161">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-161">●</span></span> |
| <span data-ttu-id="8dbb7-162">두 번째 단계로 단방향 SMS</span><span class="sxs-lookup"><span data-stu-id="8dbb7-162">One-way SMS as second factor</span></span> | <span data-ttu-id="8dbb7-163">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-163">●</span></span> | <span data-ttu-id="8dbb7-164">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-164">●</span></span> |
| <span data-ttu-id="8dbb7-165">두 번째 단계로 양방향 SMS</span><span class="sxs-lookup"><span data-stu-id="8dbb7-165">Two-way SMS as second factor</span></span> | | <span data-ttu-id="8dbb7-166">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-166">●</span></span> |
| <span data-ttu-id="8dbb7-167">두 번째 단계로 하드웨어 토큰</span><span class="sxs-lookup"><span data-stu-id="8dbb7-167">Hardware Tokens as second factor</span></span> | | <span data-ttu-id="8dbb7-168">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-168">●</span></span> |
| <span data-ttu-id="8dbb7-169">MFA를 지원하지 않는 Office 365 클라이언트에 대한 앱 암호</span><span class="sxs-lookup"><span data-stu-id="8dbb7-169">App passwords for Office 365 clients that don’t support MFA</span></span> | <span data-ttu-id="8dbb7-170">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-170">●</span></span> | |
| <span data-ttu-id="8dbb7-171">인증 방법에 대한 관리자 제어</span><span class="sxs-lookup"><span data-stu-id="8dbb7-171">Admin control over authentication methods</span></span> | <span data-ttu-id="8dbb7-172">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-172">●</span></span> | <span data-ttu-id="8dbb7-173">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-173">●</span></span> |
| <span data-ttu-id="8dbb7-174">PIN 모드</span><span class="sxs-lookup"><span data-stu-id="8dbb7-174">PIN mode</span></span> | | <span data-ttu-id="8dbb7-175">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-175">●</span></span> |
| <span data-ttu-id="8dbb7-176">사기 행위 경고</span><span class="sxs-lookup"><span data-stu-id="8dbb7-176">Fraud alert</span></span> |<span data-ttu-id="8dbb7-177">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-177">●</span></span> | <span data-ttu-id="8dbb7-178">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-178">●</span></span> |
| <span data-ttu-id="8dbb7-179">MFA 보고서</span><span class="sxs-lookup"><span data-stu-id="8dbb7-179">MFA Reports</span></span> |<span data-ttu-id="8dbb7-180">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-180">●</span></span> | <span data-ttu-id="8dbb7-181">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-181">●</span></span> |
| <span data-ttu-id="8dbb7-182">일회성 바이패스</span><span class="sxs-lookup"><span data-stu-id="8dbb7-182">One-Time Bypass</span></span> | | <span data-ttu-id="8dbb7-183">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-183">●</span></span> |
| <span data-ttu-id="8dbb7-184">전화 통화에 대한 사용자 지정 인사말</span><span class="sxs-lookup"><span data-stu-id="8dbb7-184">Custom greetings for phone calls</span></span> | <span data-ttu-id="8dbb7-185">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-185">●</span></span> | <span data-ttu-id="8dbb7-186">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-186">●</span></span> |
| <span data-ttu-id="8dbb7-187">전화 통화에 대한 사용자 지정 가능한 발신자 번호</span><span class="sxs-lookup"><span data-stu-id="8dbb7-187">Customizable caller ID for phone calls</span></span> | <span data-ttu-id="8dbb7-188">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-188">●</span></span> | <span data-ttu-id="8dbb7-189">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-189">●</span></span> |
| <span data-ttu-id="8dbb7-190">신뢰할 수 있는 IP</span><span class="sxs-lookup"><span data-stu-id="8dbb7-190">Trusted IPs</span></span> | <span data-ttu-id="8dbb7-191">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-191">●</span></span> | <span data-ttu-id="8dbb7-192">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-192">●</span></span> |
| <span data-ttu-id="8dbb7-193">신뢰할 수 있는 장치에 대한 MFA 기억</span><span class="sxs-lookup"><span data-stu-id="8dbb7-193">Remember MFA for trusted devices</span></span> | <span data-ttu-id="8dbb7-194">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-194">●</span></span> | |
| <span data-ttu-id="8dbb7-195">조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="8dbb7-195">Conditional access</span></span> | <span data-ttu-id="8dbb7-196">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-196">●</span></span> | <span data-ttu-id="8dbb7-197">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-197">●</span></span> |
| <span data-ttu-id="8dbb7-198">캐시</span><span class="sxs-lookup"><span data-stu-id="8dbb7-198">Cache</span></span> |  | <span data-ttu-id="8dbb7-199">●</span><span class="sxs-lookup"><span data-stu-id="8dbb7-199">●</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8dbb7-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8dbb7-200">Next steps</span></span>

<span data-ttu-id="8dbb7-201">클라우드 다단계 인증 또는 MFA 서버 온-프레미스 사용 여부를 결정했으므로 Azure Multi-Factor Authentication을 설정하고 사용을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dbb7-201">Now that we have determined whether to use cloud multi-factor authentication or the MFA Server on-premises, we can get started setting up and using Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="8dbb7-202">**시나리오를 나타내는 아이콘 선택**</span><span class="sxs-lookup"><span data-stu-id="8dbb7-202">**Select the icon that represents your scenario**</span></span>

<center>




<span data-ttu-id="8dbb7-203">[![클라우드](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![서버](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center></span><span class="sxs-lookup"><span data-stu-id="8dbb7-203">[![Cloud](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Server](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center></span></span>
