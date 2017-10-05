---
title: "Azure AD 응용 프로그램 프록시로 업그레이드 | Microsoft Docs"
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
ms.openlocfilehash: 6c9f70493155de6989b26fd4e8bcf1dff01c835c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="compare-remote-access-solutions"></a><span data-ttu-id="dcee1-103">원격 액세스 솔루션 비교</span><span class="sxs-lookup"><span data-stu-id="dcee1-103">Compare remote access solutions</span></span>

<span data-ttu-id="dcee1-104">Azure Active Directory 응용 프로그램 프록시는 Microsoft에서 제공하는 두 가지 원격 액세스 솔루션 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="dcee1-104">Azure Active Directory Application Proxy is one of two remote access solutions that Microsoft offers.</span></span> <span data-ttu-id="dcee1-105">다른 하나는 온-프레미스 버전인 웹 응용 프로그램 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="dcee1-105">The other is Web Application Proxy, the on-premises version.</span></span> <span data-ttu-id="dcee1-106">이 두 가지 솔루션은 이전에 Microsoft에서 제공한 제품인 Microsoft Forefront TMG(Threat Management Gateway) 및 UAG(Unified Access Gateway)를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="dcee1-106">These two solutions replace earlier products that Microsoft offered: Microsoft Forefront Threat Management Gateway (TMG) and Unified Access Gateway (UAG).</span></span> <span data-ttu-id="dcee1-107">이 문서를 사용하여 이러한 네 가지 솔루션을 서로 비교하는 방법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="dcee1-107">Use this article to understand how these four solutions compare to each other.</span></span> <span data-ttu-id="dcee1-108">사용되지 않는 TMG 또는 UAG 솔루션을 아직도 사용하는 경우 이 문서를 사용하여 응용 프로그램 프록시 중 하나로 마이그레이션하는 계획을 세워보세요.</span><span class="sxs-lookup"><span data-stu-id="dcee1-108">For those of you still using the deprecated TMG or UAG solutions, use this article to help plan your migration to one of the Application Proxy.</span></span> 


## <a name="feature-comparison"></a><span data-ttu-id="dcee1-109">기능 비교</span><span class="sxs-lookup"><span data-stu-id="dcee1-109">Feature comparison</span></span>

<span data-ttu-id="dcee1-110">이 표를 사용하여 TMG(Threat Management Gateway), UAG(Unified Access Gateway), WAP(웹 응용 프로그램 프록시) 및 Azure AD AP(응용 프로그램 프록시)를 서로 비교하는 방법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="dcee1-110">Use this table to understand how Threat Management Gateway (TMG), Unified Access Gateway (UAG), Web Application Proxy (WAP), and Azure AD Application Proxy (AP) compare to each other.</span></span>

| <span data-ttu-id="dcee1-111">기능</span><span class="sxs-lookup"><span data-stu-id="dcee1-111">Feature</span></span> | <span data-ttu-id="dcee1-112">TMG</span><span class="sxs-lookup"><span data-stu-id="dcee1-112">TMG</span></span> | <span data-ttu-id="dcee1-113">UAG</span><span class="sxs-lookup"><span data-stu-id="dcee1-113">UAG</span></span> | <span data-ttu-id="dcee1-114">WAP</span><span class="sxs-lookup"><span data-stu-id="dcee1-114">WAP</span></span> | <span data-ttu-id="dcee1-115">AP</span><span class="sxs-lookup"><span data-stu-id="dcee1-115">AP</span></span> |
| ------- | --- | --- | --- | --- |
| <span data-ttu-id="dcee1-116">인증서 인증</span><span class="sxs-lookup"><span data-stu-id="dcee1-116">Certificate authentication</span></span> | <span data-ttu-id="dcee1-117">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-117">Yes</span></span> | <span data-ttu-id="dcee1-118">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-118">Yes</span></span> | - | - |
| <span data-ttu-id="dcee1-119">선택적으로 브라우저 앱 게시</span><span class="sxs-lookup"><span data-stu-id="dcee1-119">Selectively publish browser apps</span></span> | <span data-ttu-id="dcee1-120">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-120">Yes</span></span> | <span data-ttu-id="dcee1-121">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-121">Yes</span></span> | <span data-ttu-id="dcee1-122">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-122">Yes</span></span> | <span data-ttu-id="dcee1-123">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-123">Yes</span></span> |
| <span data-ttu-id="dcee1-124">사전 인증 및 Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dcee1-124">Preauthentication and single sign-on</span></span> | <span data-ttu-id="dcee1-125">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-125">Yes</span></span> | <span data-ttu-id="dcee1-126">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-126">Yes</span></span> | <span data-ttu-id="dcee1-127">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-127">Yes</span></span> | <span data-ttu-id="dcee1-128">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-128">Yes</span></span> | 
| <span data-ttu-id="dcee1-129">계층 2/3 방화벽</span><span class="sxs-lookup"><span data-stu-id="dcee1-129">Layer 2/3 firewall</span></span> | <span data-ttu-id="dcee1-130">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-130">Yes</span></span> | <span data-ttu-id="dcee1-131">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-131">Yes</span></span> | - | - |
| <span data-ttu-id="dcee1-132">전달 프록시 기능</span><span class="sxs-lookup"><span data-stu-id="dcee1-132">Forward proxy capabilities</span></span> | <span data-ttu-id="dcee1-133">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-133">Yes</span></span> | - | - | - |
| <span data-ttu-id="dcee1-134">VPN 기능</span><span class="sxs-lookup"><span data-stu-id="dcee1-134">VPN capabilities</span></span> | <span data-ttu-id="dcee1-135">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-135">Yes</span></span> | <span data-ttu-id="dcee1-136">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-136">Yes</span></span> | - | - |
| <span data-ttu-id="dcee1-137">다양한 프로토콜 지원</span><span class="sxs-lookup"><span data-stu-id="dcee1-137">Rich protocol support</span></span> | - | <span data-ttu-id="dcee1-138">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-138">Yes</span></span> | <span data-ttu-id="dcee1-139">예, HTTP를 통해 실행하는 경우</span><span class="sxs-lookup"><span data-stu-id="dcee1-139">Yes, if running over HTTP</span></span> | <span data-ttu-id="dcee1-140">예, HTTP 또는 원격 데스크톱 게이트웨이를 통해 실행하는 경우</span><span class="sxs-lookup"><span data-stu-id="dcee1-140">Yes, if running over HTTP or through Remote Desktop Gateway</span></span> |
| <span data-ttu-id="dcee1-141">ADFS 프록시 서버 역할 수행</span><span class="sxs-lookup"><span data-stu-id="dcee1-141">Serves as ADFS proxy server</span></span> | - | <span data-ttu-id="dcee1-142">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-142">Yes</span></span> | <span data-ttu-id="dcee1-143">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-143">Yes</span></span> | - |
| <span data-ttu-id="dcee1-144">응용 프로그램 액세스에 대한 단일 포털</span><span class="sxs-lookup"><span data-stu-id="dcee1-144">One portal for application access</span></span> | - | <span data-ttu-id="dcee1-145">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-145">Yes</span></span> | - | <span data-ttu-id="dcee1-146">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-146">Yes</span></span> |
| <span data-ttu-id="dcee1-147">응답 본문 링크 변환</span><span class="sxs-lookup"><span data-stu-id="dcee1-147">Response body link translation</span></span> | <span data-ttu-id="dcee1-148">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-148">Yes</span></span> | <span data-ttu-id="dcee1-149">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-149">Yes</span></span> | - | <span data-ttu-id="dcee1-150">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-150">Yes</span></span> | 
| <span data-ttu-id="dcee1-151">헤더를 사용한 인증</span><span class="sxs-lookup"><span data-stu-id="dcee1-151">Authentication with headers</span></span> | - | <span data-ttu-id="dcee1-152">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-152">Yes</span></span> | - | <span data-ttu-id="dcee1-153">예, PingAccess 사용</span><span class="sxs-lookup"><span data-stu-id="dcee1-153">Yes, with PingAccess</span></span> | 
| <span data-ttu-id="dcee1-154">클라우드 규모 보안</span><span class="sxs-lookup"><span data-stu-id="dcee1-154">Cloud-scale security</span></span> | - | - | - | <span data-ttu-id="dcee1-155">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-155">Yes</span></span> | 
| <span data-ttu-id="dcee1-156">조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="dcee1-156">Conditional access</span></span> | - | <span data-ttu-id="dcee1-157">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-157">Yes</span></span> | - | <span data-ttu-id="dcee1-158">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-158">Yes</span></span> |
| <span data-ttu-id="dcee1-159">DMZ(완충 영역)에 구성 요소 없음</span><span class="sxs-lookup"><span data-stu-id="dcee1-159">No components in the demilitarized zone (DMZ)</span></span> | - | - | - | <span data-ttu-id="dcee1-160">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-160">Yes</span></span> |
| <span data-ttu-id="dcee1-161">인바운드 연결 없음</span><span class="sxs-lookup"><span data-stu-id="dcee1-161">No inbound connections</span></span> | - | - | - | <span data-ttu-id="dcee1-162">예</span><span class="sxs-lookup"><span data-stu-id="dcee1-162">Yes</span></span> |

<span data-ttu-id="dcee1-163">대부분의 시나리오에서 Azure AD 응용 프로그램을 최신 솔루션으로 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dcee1-163">For most scenarios, we recommend Azure AD Application as the modern solution.</span></span> <span data-ttu-id="dcee1-164">웹 응용 프로그램 프록시는 AD FS용 프록시 서버가 필요한 시나리오에서만 사용할 수 있으며, Azure Active Directory에서는 사용자 지정 도메인을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcee1-164">Web Application Proxy is only preferred in scenarios that require a proxy server for AD FS, and you can't use custom domains in Azure Active Directory.</span></span> 

<span data-ttu-id="dcee1-165">Azure AD 응용 프로그램 프록시는 유사한 제품과 비교할 때 다음을 포함한 특유의 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dcee1-165">Azure AD Application Proxy offers unique benefits when compared to similar products, including:</span></span>

- <span data-ttu-id="dcee1-166">Azure AD를 온-프레미스 리소스로 확장</span><span class="sxs-lookup"><span data-stu-id="dcee1-166">Extending Azure AD to on-premises resources</span></span>
   - <span data-ttu-id="dcee1-167">클라우드 규모 보안 및 보호</span><span class="sxs-lookup"><span data-stu-id="dcee1-167">Cloud-scale security and protection</span></span>
   - <span data-ttu-id="dcee1-168">조건부 액세스 및 Multi-Factor Authentication과 같이 쉽게 사용할 수 있는 기능</span><span class="sxs-lookup"><span data-stu-id="dcee1-168">Features like conditional access and Multi-Factor Authentication are easy to enable</span></span>
- <span data-ttu-id="dcee1-169">완충 영역에 구성 요소 없음</span><span class="sxs-lookup"><span data-stu-id="dcee1-169">No componenet in the demilitarized zone</span></span>
- <span data-ttu-id="dcee1-170">필요한 인바운드 연결 없음</span><span class="sxs-lookup"><span data-stu-id="dcee1-170">No inbound connections required</span></span>
- <span data-ttu-id="dcee1-171">사용자가 O365, Azure AD 통합 SaaS 앱 및 온-프레미스 웹앱을 포함한 모든 응용 프로그램을 사용하기 위해 이동할 수 있는 단일 액세스 패널</span><span class="sxs-lookup"><span data-stu-id="dcee1-171">One access panel that your users can go to for all their applications, including O365, Azure AD integrated SaaS apps, and your on-premises web apps.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="dcee1-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dcee1-172">Next steps</span></span>

- [<span data-ttu-id="dcee1-173">Azure AD 응용 프로그램을 사용하여 온-프레미스 응용 프로그램에 대한 보안된 원격 액세스를 제공하는 방법</span><span class="sxs-lookup"><span data-stu-id="dcee1-173">Use Azure AD Application to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- <span data-ttu-id="dcee1-174">[Forefront TMG 및 UAG에서 응용 프로그램 프록시로 전환(영문)](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/)</span><span class="sxs-lookup"><span data-stu-id="dcee1-174">[Transition from Forefront TMG and UAG to Application Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).</span></span>
