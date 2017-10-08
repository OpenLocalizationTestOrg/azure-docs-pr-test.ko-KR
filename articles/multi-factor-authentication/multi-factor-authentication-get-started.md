---
title: "Azure MFA 클라우드 또는 서버 사이의 aaaChoose | Microsoft Docs"
description: "이 적합 한지를 요청 하 여 내 사용자가 현재 위치 및 toosecure 시도 I에 있는 어떤 오전 hello multi-factor authentication 보안 솔루션을 선택 합니다.  클라우드, MFA 서버 또는 AD FS를 선택합니다."
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
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a><span data-ttu-id="3320c-104">Hello Azure Multi-factor Authentication 솔루션 선택</span><span class="sxs-lookup"><span data-stu-id="3320c-104">Choose hello Azure Multi-Factor Authentication solution for you</span></span>
<span data-ttu-id="3320c-105">있기 때문에 여러 버전의 Azure Multi-factor Authentication (MFA), 버전을 적절 한 toouse hello 몇 가지 질문 toofigure를 대답 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3320c-105">Because there are several flavors of Azure Multi-Factor Authentication (MFA), we must answer a few questions toofigure out which version is hello proper one toouse.</span></span>  <span data-ttu-id="3320c-106">해당 질문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3320c-106">Those questions are:</span></span>

* [<span data-ttu-id="3320c-107">어떤 toosecure 려 하는데</span><span class="sxs-lookup"><span data-stu-id="3320c-107">What am I trying toosecure</span></span>](#what-am-i-trying-to-secure)
* [<span data-ttu-id="3320c-108">Hello 사용자는 어디에 있습니까</span><span class="sxs-lookup"><span data-stu-id="3320c-108">Where are hello users located</span></span>](#where-are-the-users-located)
* [<span data-ttu-id="3320c-109">어떤 기능이 필요합니까?</span><span class="sxs-lookup"><span data-stu-id="3320c-109">What features do I need?</span></span>](#what-featured-do-i-need)

<span data-ttu-id="3320c-110">hello 다음 섹션에서는 한 지침을 제공 각 이러한 응답을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3320c-110">hello following sections provide guidance on determining each of these answers.</span></span>

## <a name="what-am-i-trying-toosecure"></a><span data-ttu-id="3320c-111">어떤 toosecure 시도 있습니까?</span><span class="sxs-lookup"><span data-stu-id="3320c-111">What am I trying toosecure?</span></span>
<span data-ttu-id="3320c-112">toodetermine hello 올바른 2 단계 확인 솔루션을 먼저 우리 질문에 대답 해야 hello 무엇 인가 하는 동안 toosecure 보조 인증 방법 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3320c-112">toodetermine hello correct two-step verification solution, first we must answer hello question of what are you trying toosecure with a second method of authentication.</span></span>  <span data-ttu-id="3320c-113">Azure에 있는 응용프로그램입니까?</span><span class="sxs-lookup"><span data-stu-id="3320c-113">Is it an application that is in Azure?</span></span>  <span data-ttu-id="3320c-114">또는 원격 액세스 시스템입니까?</span><span class="sxs-lookup"><span data-stu-id="3320c-114">Or a remote access system?</span></span>  <span data-ttu-id="3320c-115">항목을 파악 함으로써 포함 상태 toosecure, Multi-factor Authentication toobe 사용 하도록 설정 해야 하는 위치의 hello 질문에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3320c-115">By determining what we are trying toosecure, we can answer hello question of where Multi-Factor Authentication needs toobe enabled.</span></span>  

| <span data-ttu-id="3320c-116">동안 toosecure 무엇입니까</span><span class="sxs-lookup"><span data-stu-id="3320c-116">What are you trying toosecure</span></span> | <span data-ttu-id="3320c-117">Hello 클라우드에서 MFA</span><span class="sxs-lookup"><span data-stu-id="3320c-117">MFA in hello cloud</span></span> | <span data-ttu-id="3320c-118">MFA 서버 </span><span class="sxs-lookup"><span data-stu-id="3320c-118">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="3320c-119">자사 Microsoft 앱</span><span class="sxs-lookup"><span data-stu-id="3320c-119">First-party Microsoft apps</span></span> |<span data-ttu-id="3320c-120">●</span><span class="sxs-lookup"><span data-stu-id="3320c-120">●</span></span> |<span data-ttu-id="3320c-121">●</span><span class="sxs-lookup"><span data-stu-id="3320c-121">●</span></span> |
| <span data-ttu-id="3320c-122">Hello 응용 프로그램 갤러리에서 SaaS 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="3320c-122">SaaS apps in hello app gallery</span></span> |<span data-ttu-id="3320c-123">●</span><span class="sxs-lookup"><span data-stu-id="3320c-123">●</span></span> |  |
| <span data-ttu-id="3320c-124">Azure AD 앱 프록시를 통해 웹 응용프로그램 게시됨</span><span class="sxs-lookup"><span data-stu-id="3320c-124">Web applications published through Azure AD App Proxy</span></span> |<span data-ttu-id="3320c-125">●</span><span class="sxs-lookup"><span data-stu-id="3320c-125">●</span></span> |  |
| <span data-ttu-id="3320c-126">Azure AD 응용프로그램 프록시를 통해 IIS 응용프로그램 게시되지 않음</span><span class="sxs-lookup"><span data-stu-id="3320c-126">IIS applications not published through Azure AD App Proxy</span></span> | |<span data-ttu-id="3320c-127">●</span><span class="sxs-lookup"><span data-stu-id="3320c-127">●</span></span> |
| <span data-ttu-id="3320c-128">VPN, RDG와 같은 원격 액세스</span><span class="sxs-lookup"><span data-stu-id="3320c-128">Remote access such as VPN, RDG</span></span> | <span data-ttu-id="3320c-129">●</span><span class="sxs-lookup"><span data-stu-id="3320c-129">●</span></span> | <span data-ttu-id="3320c-130">●</span><span class="sxs-lookup"><span data-stu-id="3320c-130">●</span></span> |

## <a name="where-are-hello-users-located"></a><span data-ttu-id="3320c-131">Hello 사용자는 어디에 있습니까</span><span class="sxs-lookup"><span data-stu-id="3320c-131">Where are hello users located</span></span>
<span data-ttu-id="3320c-132">다음으로, 사용자에 게 있는 보면 hello 클라우드에 관계 없이 toodetermine hello 올바른 솔루션 toouse 있습니다 또는 온-프레미스를 사용 하 여 MFA 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3320c-132">Next, looking at where our users are located helps toodetermine hello correct solution toouse, whether in hello cloud or on-premises using hello MFA Server.</span></span>

| <span data-ttu-id="3320c-133">사용자 위치</span><span class="sxs-lookup"><span data-stu-id="3320c-133">User Location</span></span> | <span data-ttu-id="3320c-134">Hello 클라우드에서 MFA</span><span class="sxs-lookup"><span data-stu-id="3320c-134">MFA in hello cloud</span></span> | <span data-ttu-id="3320c-135">MFA 서버 </span><span class="sxs-lookup"><span data-stu-id="3320c-135">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="3320c-136">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3320c-136">Azure Active Directory</span></span> |<span data-ttu-id="3320c-137">●</span><span class="sxs-lookup"><span data-stu-id="3320c-137">●</span></span> | |
| <span data-ttu-id="3320c-138">Azure AD 및 AD FS로 페더레이션을 사용한 온-프레미스 AD</span><span class="sxs-lookup"><span data-stu-id="3320c-138">Azure AD and on-premises AD using federation with AD FS</span></span> |<span data-ttu-id="3320c-139">●</span><span class="sxs-lookup"><span data-stu-id="3320c-139">●</span></span> |<span data-ttu-id="3320c-140">●</span><span class="sxs-lookup"><span data-stu-id="3320c-140">●</span></span> |
| <span data-ttu-id="3320c-141">Azure AD 및 DirSync를 사용한 온-프레미스 AD, Azure AD Sync, Azure AD Connect - 암호 동기화 없음</span><span class="sxs-lookup"><span data-stu-id="3320c-141">Azure AD and on-premises AD using DirSync, Azure AD Sync, Azure AD Connect - no password sync</span></span> |<span data-ttu-id="3320c-142">●</span><span class="sxs-lookup"><span data-stu-id="3320c-142">●</span></span> |<span data-ttu-id="3320c-143">●</span><span class="sxs-lookup"><span data-stu-id="3320c-143">●</span></span> |
| <span data-ttu-id="3320c-144">Azure AD 및 DirSync를 사용한 온-프레미스 AD, Azure AD Sync, Azure AD Connect - 암호 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="3320c-144">Azure AD and on-premises AD using DirSync, Azure AD Sync, Azure AD Connect - with password sync</span></span> |<span data-ttu-id="3320c-145">●</span><span class="sxs-lookup"><span data-stu-id="3320c-145">●</span></span> | |
| <span data-ttu-id="3320c-146">온-프레미스 Active Directory</span><span class="sxs-lookup"><span data-stu-id="3320c-146">On-premises Active Directory</span></span> | |<span data-ttu-id="3320c-147">●</span><span class="sxs-lookup"><span data-stu-id="3320c-147">●</span></span> |

## <a name="what-features-do-i-need"></a><span data-ttu-id="3320c-148">어떤 기능이 필요합니까?</span><span class="sxs-lookup"><span data-stu-id="3320c-148">What features do I need?</span></span>
<span data-ttu-id="3320c-149">hello 다음 표에서 비교 hello 클라우드에서 Multi-factor authentication 및 Multi-factor Authentication 서버 hello로 사용할 수 있는 hello 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="3320c-149">hello following table compares hello features that are available with Multi-Factor Authentication in hello cloud and with hello Multi-Factor Authentication Server.</span></span>

| <span data-ttu-id="3320c-150">기능</span><span class="sxs-lookup"><span data-stu-id="3320c-150">Feature</span></span> | <span data-ttu-id="3320c-151">Hello 클라우드에서 MFA</span><span class="sxs-lookup"><span data-stu-id="3320c-151">MFA in hello cloud</span></span> | <span data-ttu-id="3320c-152">MFA 서버 </span><span class="sxs-lookup"><span data-stu-id="3320c-152">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="3320c-153">두 번째 단계로 모바일 앱 알림</span><span class="sxs-lookup"><span data-stu-id="3320c-153">Mobile app notification as a second factor</span></span> | <span data-ttu-id="3320c-154">●</span><span class="sxs-lookup"><span data-stu-id="3320c-154">●</span></span> | <span data-ttu-id="3320c-155">●</span><span class="sxs-lookup"><span data-stu-id="3320c-155">●</span></span> |
| <span data-ttu-id="3320c-156">두 번째 단계로 모바일 앱 확인 코드</span><span class="sxs-lookup"><span data-stu-id="3320c-156">Mobile app verification code as a second factor</span></span> | <span data-ttu-id="3320c-157">●</span><span class="sxs-lookup"><span data-stu-id="3320c-157">●</span></span> | <span data-ttu-id="3320c-158">●</span><span class="sxs-lookup"><span data-stu-id="3320c-158">●</span></span> |
| <span data-ttu-id="3320c-159">두 번째 단계로 전화 통화</span><span class="sxs-lookup"><span data-stu-id="3320c-159">Phone call as second factor</span></span> | <span data-ttu-id="3320c-160">●</span><span class="sxs-lookup"><span data-stu-id="3320c-160">●</span></span> | <span data-ttu-id="3320c-161">●</span><span class="sxs-lookup"><span data-stu-id="3320c-161">●</span></span> |
| <span data-ttu-id="3320c-162">두 번째 단계로 단방향 SMS</span><span class="sxs-lookup"><span data-stu-id="3320c-162">One-way SMS as second factor</span></span> | <span data-ttu-id="3320c-163">●</span><span class="sxs-lookup"><span data-stu-id="3320c-163">●</span></span> | <span data-ttu-id="3320c-164">●</span><span class="sxs-lookup"><span data-stu-id="3320c-164">●</span></span> |
| <span data-ttu-id="3320c-165">두 번째 단계로 양방향 SMS</span><span class="sxs-lookup"><span data-stu-id="3320c-165">Two-way SMS as second factor</span></span> | | <span data-ttu-id="3320c-166">●</span><span class="sxs-lookup"><span data-stu-id="3320c-166">●</span></span> |
| <span data-ttu-id="3320c-167">두 번째 단계로 하드웨어 토큰</span><span class="sxs-lookup"><span data-stu-id="3320c-167">Hardware Tokens as second factor</span></span> | | <span data-ttu-id="3320c-168">●</span><span class="sxs-lookup"><span data-stu-id="3320c-168">●</span></span> |
| <span data-ttu-id="3320c-169">MFA를 지원하지 않는 Office 365 클라이언트에 대한 앱 암호</span><span class="sxs-lookup"><span data-stu-id="3320c-169">App passwords for Office 365 clients that don’t support MFA</span></span> | <span data-ttu-id="3320c-170">●</span><span class="sxs-lookup"><span data-stu-id="3320c-170">●</span></span> | |
| <span data-ttu-id="3320c-171">인증 방법에 대한 관리자 제어</span><span class="sxs-lookup"><span data-stu-id="3320c-171">Admin control over authentication methods</span></span> | <span data-ttu-id="3320c-172">●</span><span class="sxs-lookup"><span data-stu-id="3320c-172">●</span></span> | <span data-ttu-id="3320c-173">●</span><span class="sxs-lookup"><span data-stu-id="3320c-173">●</span></span> |
| <span data-ttu-id="3320c-174">PIN 모드</span><span class="sxs-lookup"><span data-stu-id="3320c-174">PIN mode</span></span> | | <span data-ttu-id="3320c-175">●</span><span class="sxs-lookup"><span data-stu-id="3320c-175">●</span></span> |
| <span data-ttu-id="3320c-176">사기 행위 경고</span><span class="sxs-lookup"><span data-stu-id="3320c-176">Fraud alert</span></span> |<span data-ttu-id="3320c-177">●</span><span class="sxs-lookup"><span data-stu-id="3320c-177">●</span></span> | <span data-ttu-id="3320c-178">●</span><span class="sxs-lookup"><span data-stu-id="3320c-178">●</span></span> |
| <span data-ttu-id="3320c-179">MFA 보고서</span><span class="sxs-lookup"><span data-stu-id="3320c-179">MFA Reports</span></span> |<span data-ttu-id="3320c-180">●</span><span class="sxs-lookup"><span data-stu-id="3320c-180">●</span></span> | <span data-ttu-id="3320c-181">●</span><span class="sxs-lookup"><span data-stu-id="3320c-181">●</span></span> |
| <span data-ttu-id="3320c-182">일회성 바이패스</span><span class="sxs-lookup"><span data-stu-id="3320c-182">One-Time Bypass</span></span> | | <span data-ttu-id="3320c-183">●</span><span class="sxs-lookup"><span data-stu-id="3320c-183">●</span></span> |
| <span data-ttu-id="3320c-184">전화 통화에 대한 사용자 지정 인사말</span><span class="sxs-lookup"><span data-stu-id="3320c-184">Custom greetings for phone calls</span></span> | <span data-ttu-id="3320c-185">●</span><span class="sxs-lookup"><span data-stu-id="3320c-185">●</span></span> | <span data-ttu-id="3320c-186">●</span><span class="sxs-lookup"><span data-stu-id="3320c-186">●</span></span> |
| <span data-ttu-id="3320c-187">전화 통화에 대한 사용자 지정 가능한 발신자 번호</span><span class="sxs-lookup"><span data-stu-id="3320c-187">Customizable caller ID for phone calls</span></span> | <span data-ttu-id="3320c-188">●</span><span class="sxs-lookup"><span data-stu-id="3320c-188">●</span></span> | <span data-ttu-id="3320c-189">●</span><span class="sxs-lookup"><span data-stu-id="3320c-189">●</span></span> |
| <span data-ttu-id="3320c-190">신뢰할 수 있는 IP</span><span class="sxs-lookup"><span data-stu-id="3320c-190">Trusted IPs</span></span> | <span data-ttu-id="3320c-191">●</span><span class="sxs-lookup"><span data-stu-id="3320c-191">●</span></span> | <span data-ttu-id="3320c-192">●</span><span class="sxs-lookup"><span data-stu-id="3320c-192">●</span></span> |
| <span data-ttu-id="3320c-193">신뢰할 수 있는 장치에 대한 MFA 기억</span><span class="sxs-lookup"><span data-stu-id="3320c-193">Remember MFA for trusted devices</span></span> | <span data-ttu-id="3320c-194">●</span><span class="sxs-lookup"><span data-stu-id="3320c-194">●</span></span> | |
| <span data-ttu-id="3320c-195">조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="3320c-195">Conditional access</span></span> | <span data-ttu-id="3320c-196">●</span><span class="sxs-lookup"><span data-stu-id="3320c-196">●</span></span> | <span data-ttu-id="3320c-197">●</span><span class="sxs-lookup"><span data-stu-id="3320c-197">●</span></span> |
| <span data-ttu-id="3320c-198">캐시</span><span class="sxs-lookup"><span data-stu-id="3320c-198">Cache</span></span> |  | <span data-ttu-id="3320c-199">●</span><span class="sxs-lookup"><span data-stu-id="3320c-199">●</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3320c-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3320c-200">Next steps</span></span>

<span data-ttu-id="3320c-201">toouse multi-factor authentication 또는 hello와 MFA 서버 온-프레미스 클라우드, 여부에서는 시작할 수를 설정 하 고 Azure Multi-factor Authentication을 사용 하 여 있음을 확인 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3320c-201">Now that we have determined whether toouse cloud multi-factor authentication or hello MFA Server on-premises, we can get started setting up and using Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="3320c-202">**시나리오를 나타내는 hello 아이콘을 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3320c-202">**Select hello icon that represents your scenario**</span></span>

<center>




<span data-ttu-id="3320c-203">[![클라우드](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![서버](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center></span><span class="sxs-lookup"><span data-stu-id="3320c-203">[![Cloud](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Server](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center></span></span>
