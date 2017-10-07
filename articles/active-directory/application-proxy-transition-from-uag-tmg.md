---
title: "aaaUpgrade tooAzure AD 응용 프로그램 프록시 | Microsoft Docs"
description: "Microsoft Forefront 또는 Unified Access Gateway를 업그레이드하는 경우 가장 좋은 프록시 솔루션을 선택합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a><span data-ttu-id="9b8d6-103">원격 액세스 솔루션 비교</span><span class="sxs-lookup"><span data-stu-id="9b8d6-103">Compare remote access solutions</span></span>

<span data-ttu-id="9b8d6-104">Azure Active Directory 응용 프로그램 프록시는 Microsoft에서 제공하는 두 가지 원격 액세스 솔루션 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-104">Azure Active Directory Application Proxy is one of two remote access solutions that Microsoft offers.</span></span> <span data-ttu-id="9b8d6-105">다른 hello는 웹 응용 프로그램 프록시, hello 온-프레미스 버전.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-105">hello other is Web Application Proxy, hello on-premises version.</span></span> <span data-ttu-id="9b8d6-106">이 두 가지 솔루션은 이전에 Microsoft에서 제공한 제품인 Microsoft Forefront TMG(Threat Management Gateway) 및 UAG(Unified Access Gateway)를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-106">These two solutions replace earlier products that Microsoft offered: Microsoft Forefront Threat Management Gateway (TMG) and Unified Access Gateway (UAG).</span></span> <span data-ttu-id="9b8d6-107">이 문서 toounderstand를 사용 하 여 이러한 네 가지 솔루션에서 다른 tooeach를 비교 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-107">Use this article toounderstand how these four solutions compare tooeach other.</span></span> <span data-ttu-id="9b8d6-108">경우 여전히 hello를 사용 하 여 더 이상 사용 되지 TMG 또는 UAG 솔루션의 응용 프로그램 프록시 hello 프로그램 마이그레이션 tooone이 문서 toohelp 계획을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-108">For those of you still using hello deprecated TMG or UAG solutions, use this article toohelp plan your migration tooone of hello Application Proxy.</span></span> 


## <a name="feature-comparison"></a><span data-ttu-id="9b8d6-109">기능 비교</span><span class="sxs-lookup"><span data-stu-id="9b8d6-109">Feature comparison</span></span>

<span data-ttu-id="9b8d6-110">이 테이블 toounderstand를 사용 하 여 게이트웨이 TMG (Threat Management), Unified Access Gateway (UAG), 응용 프로그램 프록시 WAP (웹), 및 Azure AD 응용 프로그램 프록시 (AP) 비교 tooeach 다른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-110">Use this table toounderstand how Threat Management Gateway (TMG), Unified Access Gateway (UAG), Web Application Proxy (WAP), and Azure AD Application Proxy (AP) compare tooeach other.</span></span>

| <span data-ttu-id="9b8d6-111">기능</span><span class="sxs-lookup"><span data-stu-id="9b8d6-111">Feature</span></span> | <span data-ttu-id="9b8d6-112">TMG</span><span class="sxs-lookup"><span data-stu-id="9b8d6-112">TMG</span></span> | <span data-ttu-id="9b8d6-113">UAG</span><span class="sxs-lookup"><span data-stu-id="9b8d6-113">UAG</span></span> | <span data-ttu-id="9b8d6-114">WAP</span><span class="sxs-lookup"><span data-stu-id="9b8d6-114">WAP</span></span> | <span data-ttu-id="9b8d6-115">AP</span><span class="sxs-lookup"><span data-stu-id="9b8d6-115">AP</span></span> |
| ------- | --- | --- | --- | --- |
| <span data-ttu-id="9b8d6-116">인증서 인증</span><span class="sxs-lookup"><span data-stu-id="9b8d6-116">Certificate authentication</span></span> | <span data-ttu-id="9b8d6-117">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-117">Yes</span></span> | <span data-ttu-id="9b8d6-118">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-118">Yes</span></span> | - | - |
| <span data-ttu-id="9b8d6-119">선택적으로 브라우저 앱 게시</span><span class="sxs-lookup"><span data-stu-id="9b8d6-119">Selectively publish browser apps</span></span> | <span data-ttu-id="9b8d6-120">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-120">Yes</span></span> | <span data-ttu-id="9b8d6-121">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-121">Yes</span></span> | <span data-ttu-id="9b8d6-122">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-122">Yes</span></span> | <span data-ttu-id="9b8d6-123">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-123">Yes</span></span> |
| <span data-ttu-id="9b8d6-124">사전 인증 및 Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9b8d6-124">Preauthentication and single sign-on</span></span> | <span data-ttu-id="9b8d6-125">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-125">Yes</span></span> | <span data-ttu-id="9b8d6-126">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-126">Yes</span></span> | <span data-ttu-id="9b8d6-127">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-127">Yes</span></span> | <span data-ttu-id="9b8d6-128">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-128">Yes</span></span> | 
| <span data-ttu-id="9b8d6-129">계층 2/3 방화벽</span><span class="sxs-lookup"><span data-stu-id="9b8d6-129">Layer 2/3 firewall</span></span> | <span data-ttu-id="9b8d6-130">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-130">Yes</span></span> | <span data-ttu-id="9b8d6-131">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-131">Yes</span></span> | - | - |
| <span data-ttu-id="9b8d6-132">전달 프록시 기능</span><span class="sxs-lookup"><span data-stu-id="9b8d6-132">Forward proxy capabilities</span></span> | <span data-ttu-id="9b8d6-133">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-133">Yes</span></span> | - | - | - |
| <span data-ttu-id="9b8d6-134">VPN 기능</span><span class="sxs-lookup"><span data-stu-id="9b8d6-134">VPN capabilities</span></span> | <span data-ttu-id="9b8d6-135">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-135">Yes</span></span> | <span data-ttu-id="9b8d6-136">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-136">Yes</span></span> | - | - |
| <span data-ttu-id="9b8d6-137">다양한 프로토콜 지원</span><span class="sxs-lookup"><span data-stu-id="9b8d6-137">Rich protocol support</span></span> | - | <span data-ttu-id="9b8d6-138">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-138">Yes</span></span> | <span data-ttu-id="9b8d6-139">예, HTTP를 통해 실행하는 경우</span><span class="sxs-lookup"><span data-stu-id="9b8d6-139">Yes, if running over HTTP</span></span> | <span data-ttu-id="9b8d6-140">예, HTTP 또는 원격 데스크톱 게이트웨이를 통해 실행하는 경우</span><span class="sxs-lookup"><span data-stu-id="9b8d6-140">Yes, if running over HTTP or through Remote Desktop Gateway</span></span> |
| <span data-ttu-id="9b8d6-141">ADFS 프록시 서버 역할 수행</span><span class="sxs-lookup"><span data-stu-id="9b8d6-141">Serves as ADFS proxy server</span></span> | - | <span data-ttu-id="9b8d6-142">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-142">Yes</span></span> | <span data-ttu-id="9b8d6-143">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-143">Yes</span></span> | - |
| <span data-ttu-id="9b8d6-144">응용 프로그램 액세스에 대한 단일 포털</span><span class="sxs-lookup"><span data-stu-id="9b8d6-144">One portal for application access</span></span> | - | <span data-ttu-id="9b8d6-145">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-145">Yes</span></span> | - | <span data-ttu-id="9b8d6-146">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-146">Yes</span></span> |
| <span data-ttu-id="9b8d6-147">응답 본문 링크 변환</span><span class="sxs-lookup"><span data-stu-id="9b8d6-147">Response body link translation</span></span> | <span data-ttu-id="9b8d6-148">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-148">Yes</span></span> | <span data-ttu-id="9b8d6-149">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-149">Yes</span></span> | - | <span data-ttu-id="9b8d6-150">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-150">Yes</span></span> | 
| <span data-ttu-id="9b8d6-151">헤더를 사용한 인증</span><span class="sxs-lookup"><span data-stu-id="9b8d6-151">Authentication with headers</span></span> | - | <span data-ttu-id="9b8d6-152">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-152">Yes</span></span> | - | <span data-ttu-id="9b8d6-153">예, PingAccess 사용</span><span class="sxs-lookup"><span data-stu-id="9b8d6-153">Yes, with PingAccess</span></span> | 
| <span data-ttu-id="9b8d6-154">클라우드 규모 보안</span><span class="sxs-lookup"><span data-stu-id="9b8d6-154">Cloud-scale security</span></span> | - | - | - | <span data-ttu-id="9b8d6-155">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-155">Yes</span></span> | 
| <span data-ttu-id="9b8d6-156">조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="9b8d6-156">Conditional access</span></span> | - | <span data-ttu-id="9b8d6-157">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-157">Yes</span></span> | - | <span data-ttu-id="9b8d6-158">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-158">Yes</span></span> |
| <span data-ttu-id="9b8d6-159">Hello 완충 영역 (DMZ)에 구성 요소가 없습니다</span><span class="sxs-lookup"><span data-stu-id="9b8d6-159">No components in hello demilitarized zone (DMZ)</span></span> | - | - | - | <span data-ttu-id="9b8d6-160">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-160">Yes</span></span> |
| <span data-ttu-id="9b8d6-161">인바운드 연결 없음</span><span class="sxs-lookup"><span data-stu-id="9b8d6-161">No inbound connections</span></span> | - | - | - | <span data-ttu-id="9b8d6-162">예</span><span class="sxs-lookup"><span data-stu-id="9b8d6-162">Yes</span></span> |

<span data-ttu-id="9b8d6-163">대부분의 시나리오에 대 한 hello 최신 솔루션으로 Azure AD 응용 프로그램을 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-163">For most scenarios, we recommend Azure AD Application as hello modern solution.</span></span> <span data-ttu-id="9b8d6-164">웹 응용 프로그램 프록시는 AD FS용 프록시 서버가 필요한 시나리오에서만 사용할 수 있으며, Azure Active Directory에서는 사용자 지정 도메인을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-164">Web Application Proxy is only preferred in scenarios that require a proxy server for AD FS, and you can't use custom domains in Azure Active Directory.</span></span> 

<span data-ttu-id="9b8d6-165">Azure AD 응용 프로그램 프록시 제공 될 때 고유한 유리 toosimilar 제품을 포함 하 여 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-165">Azure AD Application Proxy offers unique benefits when compared toosimilar products, including:</span></span>

- <span data-ttu-id="9b8d6-166">Azure AD tooon 온-프레미스 리소스를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-166">Extending Azure AD tooon-premises resources</span></span>
   - <span data-ttu-id="9b8d6-167">클라우드 규모 보안 및 보호</span><span class="sxs-lookup"><span data-stu-id="9b8d6-167">Cloud-scale security and protection</span></span>
   - <span data-ttu-id="9b8d6-168">조건부 액세스 및 Multi-factor Authentication과 같은 기능에 쉽게 tooenable는</span><span class="sxs-lookup"><span data-stu-id="9b8d6-168">Features like conditional access and Multi-Factor Authentication are easy tooenable</span></span>
- <span data-ttu-id="9b8d6-169">Hello 완충 영역에 없는 계정</span><span class="sxs-lookup"><span data-stu-id="9b8d6-169">No componenet in hello demilitarized zone</span></span>
- <span data-ttu-id="9b8d6-170">필요한 인바운드 연결 없음</span><span class="sxs-lookup"><span data-stu-id="9b8d6-170">No inbound connections required</span></span>
- <span data-ttu-id="9b8d6-171">사용자가 toofor o 365를 비롯 한 모든 응용 프로그램을 이동 수, Azure AD와 SaaS 앱 통합를 온-프레미스 웹 응용 프로그램에 대 한 액세스 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-171">One access panel that your users can go toofor all their applications, including O365, Azure AD integrated SaaS apps, and your on-premises web apps.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="9b8d6-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b8d6-172">Next steps</span></span>

- [<span data-ttu-id="9b8d6-173">Azure AD 응용 프로그램 tooprovide 보안 된 원격 액세스 tooon 온-프레미스 응용 프로그램을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9b8d6-173">Use Azure AD Application tooprovide secure remote access tooon-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- <span data-ttu-id="9b8d6-174">[Forefront TMG 및 UAG tooApplication 프록시에서에서 전환](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8d6-174">[Transition from Forefront TMG and UAG tooApplication Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).</span></span>
