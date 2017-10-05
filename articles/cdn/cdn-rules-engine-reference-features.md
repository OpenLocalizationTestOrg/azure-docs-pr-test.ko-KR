---
title: "Azure CDN 규칙 엔진 기능 | Microsoft Docs"
description: "Azure CDN 규칙 엔진 일치 조건 및 기능에 대한 참조 설명서"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 6703247aa8b4a6d53ff22ea2d4f22eb4a746e370
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-features"></a><span data-ttu-id="85a7d-103">Azure CDN 규칙 엔진 기능</span><span class="sxs-lookup"><span data-stu-id="85a7d-103">Azure CDN rules engine features</span></span>
<span data-ttu-id="85a7d-104">이 문서에서는 Azure Content Delivery Network(CDN) [규칙 엔진](cdn-rules-engine.md)에 사용할 수 있는 기능에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-104">This topic lists detailed descriptions of the available features for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="85a7d-105">규칙의 세 번째 부분은 기능을 다루고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-105">The third part of a rule is the feature.</span></span> <span data-ttu-id="85a7d-106">기능은 일치 조건 집합으로 식별되는 요청 유형에 적용할 작업 유형을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-106">A feature defines the type of action that will be applied to the type of request identified by a set of match conditions.</span></span>

## <a name="access"></a><span data-ttu-id="85a7d-107">Access</span><span class="sxs-lookup"><span data-stu-id="85a7d-107">Access</span></span>

<span data-ttu-id="85a7d-108">이러한 기능은 콘텐츠에 대한 액세스를 제어하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-108">These features are designed to control access to content.</span></span>


<span data-ttu-id="85a7d-109">이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-109">Name</span></span> | <span data-ttu-id="85a7d-110">목적</span><span class="sxs-lookup"><span data-stu-id="85a7d-110">Purpose</span></span>
-----|--------
<span data-ttu-id="85a7d-111">액세스 거부</span><span class="sxs-lookup"><span data-stu-id="85a7d-111">Deny Access</span></span> | <span data-ttu-id="85a7d-112">모든 요청이 403 사용 권한 없음 응답으로 거부되는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-112">Determines whether all requests are rejected with a 403 Forbidden response.</span></span>
<span data-ttu-id="85a7d-113">토큰 인증</span><span class="sxs-lookup"><span data-stu-id="85a7d-113">Token Auth</span></span> | <span data-ttu-id="85a7d-114">요청에 토큰 기반 인증을 적용할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-114">Determines whether Token-Based Authentication will be applied to a request.</span></span>
<span data-ttu-id="85a7d-115">토큰 인증 거부 코드</span><span class="sxs-lookup"><span data-stu-id="85a7d-115">Token Auth Denial Code</span></span> | <span data-ttu-id="85a7d-116">토큰 기반 인증으로 인해 요청이 거부되는 경우 사용자에게 반환할 응답 유형을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-116">Determines the type of response that will be returned to a user when a request is denied due to Token-Based Authentication.</span></span>
<span data-ttu-id="85a7d-117">토큰 인증 URL 대/소문자 무시</span><span class="sxs-lookup"><span data-stu-id="85a7d-117">Token Auth Ignore URL Case</span></span> | <span data-ttu-id="85a7d-118">토큰 기반 인증에서 URL 비교 시 대/소문자를 구분할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-118">Determines whether URL comparisons made by Token-Based Authentication will be case-sensitive.</span></span>
<span data-ttu-id="85a7d-119">토큰 인증 매개 변수</span><span class="sxs-lookup"><span data-stu-id="85a7d-119">Token Auth Parameter</span></span> | <span data-ttu-id="85a7d-120">토큰 기반 인증 쿼리 문자열 매개 변수 이름을 바꿔야 하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-120">Determines whether the Token-Based Authentication query string parameter should be renamed.</span></span>

### <a name="deny-access"></a><span data-ttu-id="85a7d-121">액세스 거부</span><span class="sxs-lookup"><span data-stu-id="85a7d-121">Deny Access</span></span>
<span data-ttu-id="85a7d-122">**목적**: 모든 요청이 403 사용할 수 없음 응답으로 거부되는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-122">**Purpose**: Determines whether all requests are rejected with a 403 Forbidden response.</span></span>

<span data-ttu-id="85a7d-123">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-123">Value</span></span> | <span data-ttu-id="85a7d-124">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-124">Result</span></span>
------|-------
<span data-ttu-id="85a7d-125">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-125">Enabled</span></span>| <span data-ttu-id="85a7d-126">403 사용할 수 없음 응답으로 거부되는 일치 조건을 충족하는 요청을 모두 거부하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-126">Causes all requests that satisfy the matching criteria to be rejected with a 403 Forbidden response.</span></span>
<span data-ttu-id="85a7d-127">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-127">Disabled</span></span>| <span data-ttu-id="85a7d-128">기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-128">Restores the default behavior.</span></span> <span data-ttu-id="85a7d-129">기본 동작은 원본 서버에서 반환될 응답 형식을 결정할 수 있도록 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-129">The default behavior is to allow the origin server to determine the type of response that will be returned.</span></span>

<span data-ttu-id="85a7d-130">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-130">**Default Behavior**: Disabled</span></span>

> [!TIP]
   > <span data-ttu-id="85a7d-131">이 기능의 가능한 용도 한 가지는 요청 헤더 일치 조건과 연결하여 콘텐츠에 대한 인라인 링크를 사용하는 HTTP 참조 페이지에 대한 액세스를 차단하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-131">One possible use for this feature is to associate it with a Request Header match condition to block access to HTTP referrers that are using inline links to your content.</span></span>

### <a name="token-auth"></a><span data-ttu-id="85a7d-132">토큰 인증</span><span class="sxs-lookup"><span data-stu-id="85a7d-132">Token Auth</span></span>
<span data-ttu-id="85a7d-133">**목적:** 요청에 토큰 기반 인증을 적용할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-133">**Purpose:** Determines whether Token-Based Authentication will be applied to a request.</span></span>

<span data-ttu-id="85a7d-134">토큰 기반 인증을 사용하는 경우 암호화된 토큰을 제공하고 해당 토큰에서 지정한 요구 사항을 준수하는 요청만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-134">If Token-Based Authentication is enabled, then only requests that provide an encrypted token and comply to the requirements specified by that token will be honored.</span></span>

<span data-ttu-id="85a7d-135">토큰 값을 암호화 및 암호 해독하는 데 사용되는 암호화 키는 토큰 인증 페이지의 기본 키 및 백업 키 옵션으로 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-135">The encryption key that will be used to encrypt and decrypt token values is determined by the Primary Key and the Backup Key options on the Token Auth page.</span></span> <span data-ttu-id="85a7d-136">암호화 키는 플랫폼에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-136">Keep in mind that encryption keys are platform-specific.</span></span>

<span data-ttu-id="85a7d-137">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-137">Value</span></span> | <span data-ttu-id="85a7d-138">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-138">Result</span></span>
------|---------
<span data-ttu-id="85a7d-139">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-139">Enabled</span></span> | <span data-ttu-id="85a7d-140">토큰 기반 인증으로 요청된 콘텐츠를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-140">Protects the requested content with Token-Based Authentication.</span></span> <span data-ttu-id="85a7d-141">유효한 토큰을 제공하고 요구 사항을 충족하는 클라이언트의 요청만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-141">Only requests from clients that provide a valid token and meet its requirements will be honored.</span></span> <span data-ttu-id="85a7d-142">FTP 트랜잭션은 토큰 기반 인증에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-142">FTP transactions are excluded from Token-Based Authentication.</span></span>
<span data-ttu-id="85a7d-143">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-143">Disabled</span></span>| <span data-ttu-id="85a7d-144">기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-144">Restores the default behavior.</span></span> <span data-ttu-id="85a7d-145">기본 동작은 토큰 기반 인증 구성으로 요청을 보안할 수 있도록 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-145">The default behavior is to allow your Token-Based Authentication configuration to determine whether a request will be secured.</span></span>

<span data-ttu-id="85a7d-146">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-146">**Default Behavior:** Disabled.</span></span>

###<a name="token-auth-denial-code"></a><span data-ttu-id="85a7d-147">토큰 인증 거부 코드</span><span class="sxs-lookup"><span data-stu-id="85a7d-147">Token Auth Denial Code</span></span>
<span data-ttu-id="85a7d-148">**목적:** 토큰 기반 인증에 따라 요청을 거부할 때 사용자에게 반환할 응답 형식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-148">**Purpose:** Determines the type of response that will be returned to a user when a request is denied due to Token-Based Authentication.</span></span>

<span data-ttu-id="85a7d-149">사용 가능한 응답 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-149">The available response codes are listed below.</span></span>

<span data-ttu-id="85a7d-150">응답 코드</span><span class="sxs-lookup"><span data-stu-id="85a7d-150">Response Code</span></span>|<span data-ttu-id="85a7d-151">응답 이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-151">Response Name</span></span>|<span data-ttu-id="85a7d-152">설명</span><span class="sxs-lookup"><span data-stu-id="85a7d-152">Description</span></span>
----------------|-----------|--------
<span data-ttu-id="85a7d-153">301</span><span class="sxs-lookup"><span data-stu-id="85a7d-153">301</span></span>|<span data-ttu-id="85a7d-154">영구적으로 이동됨</span><span class="sxs-lookup"><span data-stu-id="85a7d-154">Moved Permanently</span></span>|<span data-ttu-id="85a7d-155">권한이 없는 사용자를 Location 헤더에 지정된 URL로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-155">This status code redirects unauthorized users to the URL specified in the Location header.</span></span>
<span data-ttu-id="85a7d-156">302</span><span class="sxs-lookup"><span data-stu-id="85a7d-156">302</span></span>|<span data-ttu-id="85a7d-157">있음</span><span class="sxs-lookup"><span data-stu-id="85a7d-157">Found</span></span>|<span data-ttu-id="85a7d-158">권한이 없는 사용자를 Location 헤더에 지정된 URL로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-158">This status code redirects unauthorized users to the URL specified in the Location header.</span></span> <span data-ttu-id="85a7d-159">리디렉션을 수행하는 업계 표준 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-159">This status code is the industry standard method of performing a redirect.</span></span>
<span data-ttu-id="85a7d-160">307</span><span class="sxs-lookup"><span data-stu-id="85a7d-160">307</span></span>|<span data-ttu-id="85a7d-161">임시 리디렉션</span><span class="sxs-lookup"><span data-stu-id="85a7d-161">Temporary Redirect</span></span>|<span data-ttu-id="85a7d-162">권한이 없는 사용자를 Location 헤더에 지정된 URL로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-162">This status code redirects unauthorized users to the URL specified in the Location header.</span></span>
<span data-ttu-id="85a7d-163">401</span><span class="sxs-lookup"><span data-stu-id="85a7d-163">401</span></span>|<span data-ttu-id="85a7d-164">권한 없음</span><span class="sxs-lookup"><span data-stu-id="85a7d-164">Unauthorized</span></span>|<span data-ttu-id="85a7d-165">이 상태 코드를 WWW-Authenticate 응답 헤더와 결합하면 사용자에게 인증을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-165">Combining this status code with the WWW-Authenticate response header allows you to prompt a user for authentication.</span></span>
<span data-ttu-id="85a7d-166">403</span><span class="sxs-lookup"><span data-stu-id="85a7d-166">403</span></span>|<span data-ttu-id="85a7d-167">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="85a7d-167">Forbidden</span></span>|<span data-ttu-id="85a7d-168">보호된 콘텐츠에 액세스하려고 할 때 권한이 없는 사용자에게 표시할 표준 403 사용할 수 없음 상태 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-168">This is the standard 403 Forbidden status message that an unauthorized user will see when trying to access protected content.</span></span>
<span data-ttu-id="85a7d-169">404</span><span class="sxs-lookup"><span data-stu-id="85a7d-169">404</span></span>|<span data-ttu-id="85a7d-170">파일을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="85a7d-170">File Not Found</span></span>|<span data-ttu-id="85a7d-171">HTTP 클라이언트에서 서버와 통신할 수 있지만 요청한 콘텐츠를 찾을 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-171">This status code indicates that the HTTP client was able to communicate with the server, but the requested content was not found.</span></span>

#### <a name="url-redirection"></a><span data-ttu-id="85a7d-172">URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="85a7d-172">URL Redirection</span></span>

<span data-ttu-id="85a7d-173">이 기능은 3xx 상태 코드를 반환하도록 구성된 경우 사용자 정의 URL에 대한 URL 리디렉션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-173">This feature supports URL redirection to a user-defined URL when it is configured to return a 3xx status code.</span></span> <span data-ttu-id="85a7d-174">이 사용자 정의 URL은 다음 단계를 수행하여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-174">This user-defined URL can be specified by performing the following steps:</span></span>

1. <span data-ttu-id="85a7d-175">토큰 인증 거부 코드 기능에 대한 3xx 응답 코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-175">Select a 3xx response code for the Token Auth Denial Code feature.</span></span>
2. <span data-ttu-id="85a7d-176">선택적 헤더 이름 옵션에서 "Location"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-176">Select "Location" from the Optional Header Name option.</span></span>
3. <span data-ttu-id="85a7d-177">선택적 헤더 값 옵션을 원하는 URL로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-177">Set the Optional Header Value option to the desired URL.</span></span>

<span data-ttu-id="85a7d-178">URL이 3xx 상태 코드에 대해 정의되지 않은 경우 3xx 상태 코드에 대한 표준 응답 페이지를 사용자에게 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-178">If a URL is not defined for a 3xx status code, then the standard response page for a 3xx status code will be returned to the user.</span></span>

<span data-ttu-id="85a7d-179">URL 리디렉션은 3xx 응답 코드에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-179">URL redirection is only applicable for 3xx response codes.</span></span>

<span data-ttu-id="85a7d-180">선택적 헤더 값 옵션은 영숫자, 인용 부호 및 공백을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-180">The Optional Header Value option supports alphanumeric characters, quotation marks, and spaces.</span></span>

#### <a name="authentication"></a><span data-ttu-id="85a7d-181">인증</span><span class="sxs-lookup"><span data-stu-id="85a7d-181">Authentication</span></span>

<span data-ttu-id="85a7d-182">이 기능은 토큰 기반 인증으로 보호되는 콘텐츠에 대한 권한이 없는 요청에 응답할 때 WWW-Authenticate 헤더를 포함하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-182">This feature supports the capability to include the WWW-Authenticate header when responding to an unauthorized request for content protected by Token-Based Authentication.</span></span> <span data-ttu-id="85a7d-183">구성에서 WWW-Authenticate 헤더가 "basic"으로 설정된 경우 권한이 없는 사용자에게 계정 자격 증명을 입력하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-183">If the WWW-Authenticate header has been set to "basic" in your configuration, then the unauthorized user will be prompted for account credentials.</span></span>

<span data-ttu-id="85a7d-184">위의 구성은 다음 단계를 수행하여 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-184">The above configuration can be achieved by performing the following steps:</span></span>

1. <span data-ttu-id="85a7d-185">토큰 인증 거부 코드 기능의 응답 코드로 "401"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-185">Select "401" as the response code for the Token Auth Denial Code feature.</span></span>
2. <span data-ttu-id="85a7d-186">선택적 헤더 이름 옵션에서 "WWW-Authenticate"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-186">Select "WWW-Authenticate" from the Optional Header Name option.</span></span>
3. <span data-ttu-id="85a7d-187">선택적 헤더 값 옵션을 "basic"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-187">Set the Optional Header Value option to "basic."</span></span>

<span data-ttu-id="85a7d-188">WWW-Authenticate 헤더는 401 응답 코드에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-188">The WWW-Authenticate header is only applicable for 401 response codes.</span></span>

### <a name="token-auth-ignore-url-case"></a><span data-ttu-id="85a7d-189">토큰 인증 URL 대/소문자 무시</span><span class="sxs-lookup"><span data-stu-id="85a7d-189">Token Auth Ignore URL Case</span></span>
<span data-ttu-id="85a7d-190">**목적:** 토큰 기반 인증으로 수행되는 URL 비교에서 대/소문자를 구분하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-190">**Purpose:** Determines whether URL comparisons made by Token-Based Authentication will be case-sensitive.</span></span>

<span data-ttu-id="85a7d-191">이 기능으로 영향을 받는 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-191">The parameters affected by this feature are:</span></span>

- <span data-ttu-id="85a7d-192">ec_url_allow</span><span class="sxs-lookup"><span data-stu-id="85a7d-192">ec_url_allow</span></span>
- <span data-ttu-id="85a7d-193">ec_ref_allow</span><span class="sxs-lookup"><span data-stu-id="85a7d-193">ec_ref_allow</span></span>
- <span data-ttu-id="85a7d-194">ec_ref_deny</span><span class="sxs-lookup"><span data-stu-id="85a7d-194">ec_ref_deny</span></span>

<span data-ttu-id="85a7d-195">유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-195">Valid values are:</span></span>

<span data-ttu-id="85a7d-196">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-196">Value</span></span>|<span data-ttu-id="85a7d-197">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-197">Result</span></span>
---|----
<span data-ttu-id="85a7d-198">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-198">Enabled</span></span>|<span data-ttu-id="85a7d-199">토큰 기반 인증 매개 변수에 대한 URL을 비교할 때 에지 서버에서 대/소문자를 무시하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-199">Causes our edge server to ignore case when comparing URLs for Token-Based Authentication parameters.</span></span>
<span data-ttu-id="85a7d-200">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-200">Disabled</span></span>|<span data-ttu-id="85a7d-201">기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-201">Restores the default behavior.</span></span> <span data-ttu-id="85a7d-202">기본 동작은 토큰 인증을 위한 URL 비교에서 대/소문자를 구분하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-202">The default behavior is for URL comparisons for Token Authentication to be case-sensitive.</span></span>

<span data-ttu-id="85a7d-203">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-203">**Default Behavior:** Disabled.</span></span>
 
### <a name="token-auth-parameter"></a><span data-ttu-id="85a7d-204">토큰 인증 매개 변수</span><span class="sxs-lookup"><span data-stu-id="85a7d-204">Token Auth Parameter</span></span>
<span data-ttu-id="85a7d-205">**목적:** 토큰 기반 인증 쿼리 문자열 매개 변수의 이름을 바꿔야 하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-205">**Purpose:** Determines whether the Token-Based Authentication query string parameter should be renamed.</span></span>

<span data-ttu-id="85a7d-206">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-206">Key information:</span></span>

- <span data-ttu-id="85a7d-207">값 옵션은 토큰을 지정할 수 있는 쿼리 문자열 매개 변수 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-207">The Value option defines the query string parameter name through which a token may be specified.</span></span>
- <span data-ttu-id="85a7d-208">값 옵션은 "ec_token"으로 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-208">The Value option cannot be set to "ec_token."</span></span>
- <span data-ttu-id="85a7d-209">이름은 값 옵션에서만 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-209">Make sure that the name defined in the Value option only</span></span> 
- <span data-ttu-id="85a7d-210">유효한 URL 문자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-210">contains valid URL characters.</span></span>

<span data-ttu-id="85a7d-211">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-211">Value</span></span>|<span data-ttu-id="85a7d-212">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-212">Result</span></span>
----|----
<span data-ttu-id="85a7d-213">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-213">Enabled</span></span>|<span data-ttu-id="85a7d-214">값 옵션은 토큰을 정의해야 하는 쿼리 문자열 매개 변수 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-214">The Value option defines the query string parameter name through which tokens should be defined.</span></span>
<span data-ttu-id="85a7d-215">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-215">Disabled</span></span>|<span data-ttu-id="85a7d-216">토큰은 요청 URL에 정의되지 않은 쿼리 문자열 매개 변수로 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-216">A token may be specified as an undefined query string parameter in the request URL.</span></span>

<span data-ttu-id="85a7d-217">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-217">**Default Behavior:** Disabled.</span></span> <span data-ttu-id="85a7d-218">토큰은 요청 URL에 정의되지 않은 쿼리 문자열 매개 변수로 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-218">A token may be specified as an undefined query string parameter in the request URL.</span></span>

## <a name="caching"></a><span data-ttu-id="85a7d-219">구성</span><span class="sxs-lookup"><span data-stu-id="85a7d-219">Caching</span></span>

<span data-ttu-id="85a7d-220">이러한 기능은 콘텐츠가 캐시되는 시기와 방식을 사용자 지정하기 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-220">These features are designed to customize when and how content is cached.</span></span>

<span data-ttu-id="85a7d-221">이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-221">Name</span></span> | <span data-ttu-id="85a7d-222">목적</span><span class="sxs-lookup"><span data-stu-id="85a7d-222">Purpose</span></span>
-----|--------
<span data-ttu-id="85a7d-223">대역폭 매개 변수</span><span class="sxs-lookup"><span data-stu-id="85a7d-223">Bandwidth Parameters</span></span> | <span data-ttu-id="85a7d-224">대역폭 제한 매개 변수(예: ec_rate 및 ec_prebuf)를 활성화할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-224">Determines whether bandwidth throttling parameters (i.e., ec_rate and ec_prebuf) will be active.</span></span>
<span data-ttu-id="85a7d-225">대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="85a7d-225">Bandwidth Throttling</span></span> | <span data-ttu-id="85a7d-226">에지 서버에서 제공하는 응답에 대한 대역폭을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-226">Throttles the bandwidth for the response provided by our edge servers.</span></span>
<span data-ttu-id="85a7d-227">바이패스 캐시</span><span class="sxs-lookup"><span data-stu-id="85a7d-227">Bypass Cache</span></span> | <span data-ttu-id="85a7d-228">요청에서 캐싱 기술을 활용할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-228">Determines whether the request can leverage our caching technology.</span></span>
<span data-ttu-id="85a7d-229">Cache-Control 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="85a7d-229">Cache-Control Header Treatment</span></span> | <span data-ttu-id="85a7d-230">외부 Max-Age 기능이 활성 상태일 때 에지 서버에 의한 Cache-Control 헤더의 생성을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-230">Controls the generation of Cache-Control headers by the edge server when External Max-Age feature is active.</span></span>
<span data-ttu-id="85a7d-231">Cache-Key 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="85a7d-231">Cache-Key Query String</span></span> | <span data-ttu-id="85a7d-232">cache-key에서 요청과 관련된 쿼리 문자열 매개 변수를 포함 또는 제외할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-232">Determines whether the cache-key will include or exclude query string parameters associated with a request.</span></span>
<span data-ttu-id="85a7d-233">Cache-Key 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-233">Cache-Key Rewrite</span></span> | <span data-ttu-id="85a7d-234">요청과 관련된 cache-key를 다시 씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-234">Rewrites the cache-key associated with a request.</span></span>
<span data-ttu-id="85a7d-235">전체 캐시 채우기</span><span class="sxs-lookup"><span data-stu-id="85a7d-235">Complete Cache Fill</span></span> | <span data-ttu-id="85a7d-236">요청 결과, 에지 서버에서 캐시가 부분적으로 누락된 경우 수행할 작업을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-236">Determines what happens when a request results in a partial cache miss on an edge server.</span></span>
<span data-ttu-id="85a7d-237">압축 파일 형식</span><span class="sxs-lookup"><span data-stu-id="85a7d-237">Compress File Types</span></span> | <span data-ttu-id="85a7d-238">서버에서 압축할 파일 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-238">Defines the file formats that will be compressed on the server.</span></span>
<span data-ttu-id="85a7d-239">기본 내부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="85a7d-239">Default Internal Max-Age</span></span> | <span data-ttu-id="85a7d-240">에지 서버에서 원본 서버 캐시 유효성 재검사를 위한 기본 max-age 간격을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-240">Determines the default max-age interval for edge server to origin server cache revalidation.</span></span>
<span data-ttu-id="85a7d-241">만료 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="85a7d-241">Expires Header Treatment</span></span> | <span data-ttu-id="85a7d-242">외부 Max-Age 기능이 활성 상태일 때 에지 서버에 의한 만료 헤더의 생성을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-242">Controls the generation of Expires headers by an edge server when the External Max-Age feature is active.</span></span>
<span data-ttu-id="85a7d-243">외부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="85a7d-243">External Max-Age</span></span> | <span data-ttu-id="85a7d-244">브라우저에서 에지 서버 캐시 유효성 재검사를 위한 max-age 간격을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-244">Determines the max-age interval for browser to edge server cache revalidation.</span></span>
<span data-ttu-id="85a7d-245">강제 내부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="85a7d-245">Force Internal Max-Age</span></span> | <span data-ttu-id="85a7d-246">에지 서버에서 원본 서버 캐시 유효성 재검사를 위한 max-age 간격을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-246">Determines the max-age interval for edge server to origin server cache revalidation.</span></span>
<span data-ttu-id="85a7d-247">H.264 지원(HTTP 점진적 다운로드)</span><span class="sxs-lookup"><span data-stu-id="85a7d-247">H.264 Support (HTTP Progressive Download)</span></span> | <span data-ttu-id="85a7d-248">콘텐츠를 스트리밍하는 데 사용할 수 있는 H.264 파일 형식의 유형을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-248">Determines the types of H.264 file formats that may be used to stream content.</span></span>
<span data-ttu-id="85a7d-249">No-Cache 요청 부여</span><span class="sxs-lookup"><span data-stu-id="85a7d-249">Honor No-Cache Request</span></span> | <span data-ttu-id="85a7d-250">HTTP 클라이언트의 no-cache 요청을 원본 서버에 전달할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-250">Determines whether an HTTP client's no-cache requests will be forwarded to the origin server.</span></span>
<span data-ttu-id="85a7d-251">원본 No-Cache 무시</span><span class="sxs-lookup"><span data-stu-id="85a7d-251">Ignore Origin No-Cache</span></span> | <span data-ttu-id="85a7d-252">CDN이 원본 서버에서 제공되는 특정 지시문을 무시할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-252">Determines whether our CDN will ignore certain directives served from an origin server.</span></span>
<span data-ttu-id="85a7d-253">적절하지 않은 범위 무시</span><span class="sxs-lookup"><span data-stu-id="85a7d-253">Ignore Unsatisfiable Ranges</span></span> | <span data-ttu-id="85a7d-254">요청에서 416 요청한 범위가 적절하지 않음 상태 코드를 생성하는 경우 클라이언트로 반환할 응답을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-254">Determines the response that will be returned to clients when a request generates a 416 Requested Range Not Satisfiable status code.</span></span>
<span data-ttu-id="85a7d-255">내부 Max-Stale</span><span class="sxs-lookup"><span data-stu-id="85a7d-255">Internal Max-Stale</span></span> | <span data-ttu-id="85a7d-256">에지 서버가 원본 서버로 캐시된 자산의 유효성 재검사를 할 수 없는 경우 에지 서버에서 캐시된 자산이 정상 만료 시간을 지나 얼마나 오래 제공될 수 있는지를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-256">Controls how long past the normal expiration time a cached asset may be served from an edge server when the edge server is unable to revalidate the cached asset with the origin server.</span></span>
<span data-ttu-id="85a7d-257">부분 캐시 공유</span><span class="sxs-lookup"><span data-stu-id="85a7d-257">Partial Cache Sharing</span></span> | <span data-ttu-id="85a7d-258">요청에서 부분적으로 캐시된 콘텐츠를 생성할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-258">Determines whether a request can generate partially cached content.</span></span>
<span data-ttu-id="85a7d-259">캐시된 콘텐츠 사전 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="85a7d-259">Prevalidate Cached Content</span></span> | <span data-ttu-id="85a7d-260">TTL이 만료되기 전에 캐시된 콘텐츠로 미리 유효성 재검사할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-260">Determines whether cached content will be eligible for early revalidation before its TTL expires.</span></span>
<span data-ttu-id="85a7d-261">0바이트 캐시 파일 새로 고침</span><span class="sxs-lookup"><span data-stu-id="85a7d-261">Refresh Zero-Byte Cache Files</span></span> | <span data-ttu-id="85a7d-262">0바이트 캐시 자산에 대한 HTTP 클라이언트 요청이 에지 서버에 의해 처리되는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-262">Determines how an HTTP client's request for a 0-byte cache asset is handled by our edge servers.</span></span>
<span data-ttu-id="85a7d-263">캐시 가능한 상태 코드 집합</span><span class="sxs-lookup"><span data-stu-id="85a7d-263">Set Cacheable Status Codes</span></span> | <span data-ttu-id="85a7d-264">캐시된 콘텐츠가 발생할 수 있는 상태 코드 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-264">Defines the set of status codes that can result in cached content.</span></span>
<span data-ttu-id="85a7d-265">오류 시 오래된 콘텐츠 배달</span><span class="sxs-lookup"><span data-stu-id="85a7d-265">Stale Content Delivery on Error</span></span> | <span data-ttu-id="85a7d-266">캐시 유효성 재검사 중이나 고객 원본 서버에서 요청된 콘텐츠를 검색할 때 만료되고 캐시된 콘텐츠를 배달할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-266">Determines whether expired cached content will be delivered when an error occurs during cache revalidation or when retrieving the requested content from the customer origin server.</span></span>
<span data-ttu-id="85a7d-267">유효성 재검사 중 기한 경과</span><span class="sxs-lookup"><span data-stu-id="85a7d-267">Stale While Revalidate</span></span> | <span data-ttu-id="85a7d-268">유효성 재검사를 수행하는 동안 에지 서버가 오래된 클라이언트를 요청자에게 제공하도록 하여 성능을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-268">Improves performance by allowing our edge servers to serve stale client to the requester while revalidation takes place.</span></span>
<span data-ttu-id="85a7d-269">주석</span><span class="sxs-lookup"><span data-stu-id="85a7d-269">Comment</span></span> | <span data-ttu-id="85a7d-270">주석 기능을 통해 규칙 내에 메모를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-270">The Comment feature allows a note to be added within a rule.</span></span>

###<a name="bandwidth-parameters"></a><span data-ttu-id="85a7d-271">대역폭 매개 변수</span><span class="sxs-lookup"><span data-stu-id="85a7d-271">Bandwidth Parameters</span></span>
<span data-ttu-id="85a7d-272">**목적:** 대역폭 제한 매개 변수(예: ec_rate 및 ec_prebuf)를 활성화하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-272">**Purpose:** Determines whether bandwidth throttling parameters (i.e., ec_rate and ec_prebuf) will be active.</span></span>

<span data-ttu-id="85a7d-273">대역폭 제한 매개 변수는 클라이언트 요청에 대한 데이터 전송 속도를 사용자 지정 속도로 제한하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-273">Bandwidth throttling parameters determine whether the data transfer rate for a client's request will be limited to a custom rate.</span></span>

<span data-ttu-id="85a7d-274">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-274">Value</span></span>|<span data-ttu-id="85a7d-275">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-275">Result</span></span>
--|--
<span data-ttu-id="85a7d-276">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-276">Enabled</span></span>|<span data-ttu-id="85a7d-277">에지 서버에서 대역폭 제한 요청을 따르도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-277">Allows our edge servers to honor bandwidth throttling requests.</span></span>
<span data-ttu-id="85a7d-278">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-278">Disabled</span></span>|<span data-ttu-id="85a7d-279">에지 서버에서 대역폭 제한 매개 변수를 무시하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-279">Causes our edge servers to ignore bandwidth throttling parameters.</span></span> <span data-ttu-id="85a7d-280">요청된 콘텐츠는 대역폭 제한 없이 정상적으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-280">The requested content will be served normally (i.e., without bandwidth throttling).</span></span>

<span data-ttu-id="85a7d-281">**기본 동작**: 사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-281">**Default Behavior:** Enabled.</span></span>

###<a name="bandwidth-throttling"></a><span data-ttu-id="85a7d-282">대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="85a7d-282">Bandwidth Throttling</span></span>
<span data-ttu-id="85a7d-283">**목적:** 에지 서버에서 제공하는 응답에 대한 대역폭을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-283">**Purpose:** Throttles the bandwidth for the response provided by our edge servers.</span></span>

<span data-ttu-id="85a7d-284">대역폭 제한을 제대로 설정하려면 다음 옵션을 모두 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-284">Both of the following options must be defined to properly set up bandwidth throttling.</span></span>

<span data-ttu-id="85a7d-285">옵션</span><span class="sxs-lookup"><span data-stu-id="85a7d-285">Option</span></span>|<span data-ttu-id="85a7d-286">설명</span><span class="sxs-lookup"><span data-stu-id="85a7d-286">Description</span></span>
--|--
<span data-ttu-id="85a7d-287">초당 킬로바이트</span><span class="sxs-lookup"><span data-stu-id="85a7d-287">Kbytes per second</span></span>|<span data-ttu-id="85a7d-288">이 옵션을 응답을 전달하는 데 사용할 수 있는 최대 대역폭(Kbps)으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-288">Set this option to the maximum bandwidth (Kb per second) that may be used to deliver the response.</span></span>
<span data-ttu-id="85a7d-289">Prebuf 초</span><span class="sxs-lookup"><span data-stu-id="85a7d-289">Prebuf seconds</span></span>|<span data-ttu-id="85a7d-290">이 옵션을 에지 서버에서 대역폭을 제한할 때까지 대기하는 시간(초)으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-290">Set this option to the number of seconds that our edge servers will wait until throttling bandwidth.</span></span> <span data-ttu-id="85a7d-291">대역폭 제한이 없는 이 기간은 미디어 플레이어에서 대역폭 제한에 따른 스터터링 또는 버퍼링 문제가 발생하지 않도록 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-291">The purpose of this time period of unrestricted bandwidth is to prevent a media player from experiencing stuttering or buffering issues due to bandwidth throttling.</span></span>

<span data-ttu-id="85a7d-292">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-292">**Default Behavior:** Disabled.</span></span>

###<a name="bypass-cache"></a><span data-ttu-id="85a7d-293">바이패스 캐시</span><span class="sxs-lookup"><span data-stu-id="85a7d-293">Bypass Cache</span></span>
<span data-ttu-id="85a7d-294">**목적:** 요청에서 캐싱 기술을 활용할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-294">**Purpose:** Determines whether the request can leverage our caching technology.</span></span>

<span data-ttu-id="85a7d-295">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-295">Value</span></span>|<span data-ttu-id="85a7d-296">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-296">Result</span></span>
--|--
<span data-ttu-id="85a7d-297">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-297">Enabled</span></span>|<span data-ttu-id="85a7d-298">이전에 에지 서버에서 콘텐츠를 캐시한 경우에도 모든 요청을 원본 서버로 전달하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-298">Causes all requests to fall through to the origin server, even if the content was previously cached on edge servers.</span></span>
<span data-ttu-id="85a7d-299">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-299">Disabled</span></span>|<span data-ttu-id="85a7d-300">에지 서버에서 응답 헤더에 정의된 캐시 정책에 따라 자산을 캐시하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-300">Causes edge servers to cache assets according to the cache policy defined in its response headers.</span></span>

<span data-ttu-id="85a7d-301">**기본 동작:**</span><span class="sxs-lookup"><span data-stu-id="85a7d-301">**Default Behavior:**</span></span>

- <span data-ttu-id="85a7d-302">**HTTP Large:** 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-302">**HTTP Large:** Disabled</span></span>

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a><span data-ttu-id="85a7d-303">Cache-Control 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="85a7d-303">Cache Control Header Treatment</span></span>
<span data-ttu-id="85a7d-304">**목적:** 외부 Max-Age 기능이 활성 상태일 때 에지 서버의 Cache-Control 헤더 생성을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-304">**Purpose:** Controls the generation of Cache-Control headers by the edge server when External Max-Age Feature is active.</span></span>

<span data-ttu-id="85a7d-305">이 유형의 구성을 획득하는 가장 쉬운 방법은 동일한 문에 외부 Max-Age와 Cache-Control 헤더 처리 기능을 배치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-305">The easiest way to achieve this type of configuration is to place the External Max-Age and the Cache-Control Header Treatment features in the same statement.</span></span>

<span data-ttu-id="85a7d-306">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-306">Value</span></span>|<span data-ttu-id="85a7d-307">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-307">Result</span></span>
--|--
<span data-ttu-id="85a7d-308">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-308">Overwrite</span></span>|<span data-ttu-id="85a7d-309">다음과 같은 작업이 수행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-309">Ensures that the following actions will take place:</span></span><br/> <span data-ttu-id="85a7d-310">- 원본 서버에서 생성한 Cache-Control 헤더를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-310">- Overwrites the Cache-Control header generated by the origin server.</span></span> <br/><span data-ttu-id="85a7d-311">- 외부 Max-Age 기능으로 생성한 Cache-Control 헤더를 응답에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-311">- Adds the Cache-Control header produced by the External Max-Age feature to the response.</span></span>
<span data-ttu-id="85a7d-312">통과</span><span class="sxs-lookup"><span data-stu-id="85a7d-312">Pass Through</span></span>|<span data-ttu-id="85a7d-313">외부 Max-Age 기능으로 생성한 Cache-Control 헤더를 응답에 절대 추가하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-313">Ensures that the Cache-Control header produced by the External Max-Age feature is never added to the response.</span></span> <br/> <span data-ttu-id="85a7d-314">원본 서버에서 Cache-Control 헤더를 생성하는 경우 최종 사용자에게 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-314">If the origin server produces a Cache-Control header, it will pass through to the end-user.</span></span> <br/> <span data-ttu-id="85a7d-315">원본 서버에서 Cache-Control 헤더를 생성하지 않은 경우 이 옵션은 응답 헤더에 Cache-Control 헤더를 포함하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-315">If the origin server does not produce a Cache-Control header, then this option may cause the response header to not contain a Cache-Control header.</span></span>
<span data-ttu-id="85a7d-316">없는 경우 추가</span><span class="sxs-lookup"><span data-stu-id="85a7d-316">Add if Missing</span></span>|<span data-ttu-id="85a7d-317">Cache-Control 헤더를 원본 서버로부터 수신하지 않은 경우 이 옵션은 외부 Max-Age 기능으로 생성한 Cache-Control 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-317">If a Cache-Control header was not received from the origin server, then this option adds the Cache-Control header produced by the External Max-Age feature.</span></span> <span data-ttu-id="85a7d-318">이 옵션은 모든 자산에 Cache-Control 헤더를 할당하도록 하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-318">This option is useful for ensuring that all assets will be assigned a Cache-Control header.</span></span>
<span data-ttu-id="85a7d-319">제거</span><span class="sxs-lookup"><span data-stu-id="85a7d-319">Remove</span></span>| <span data-ttu-id="85a7d-320">헤더 응답에 Cache-Control 헤더를 포함하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-320">This option ensures that a Cache-Control header is not included with the header response.</span></span> <span data-ttu-id="85a7d-321">Cache-Control 헤더를 이미 할당한 경우 헤더 응답에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-321">If a Cache-Control header has already been assigned, then it will be stripped from the header response.</span></span>

<span data-ttu-id="85a7d-322">**기본 동작:** 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-322">**Default Behavior:** Overwrite.</span></span>

###<a name="cache-key-query-string"></a><span data-ttu-id="85a7d-323">Cache-Key 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="85a7d-323">Cache-Key Query String</span></span>
<span data-ttu-id="85a7d-324">**목적:** cache-key에서 요청과 관련된 쿼리 문자열 매개 변수를 포함할지 또는 제외할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-324">**Purpose:** Determines whether the cache-key will include or exclude query string parameters associated with a request.</span></span>

<span data-ttu-id="85a7d-325">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-325">Key information:</span></span>

- <span data-ttu-id="85a7d-326">쿼리 문자열 매개 변수 이름을 둘 이상 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-326">Specify one or more query string parameter name(s).</span></span> <span data-ttu-id="85a7d-327">각 매개 변수 이름은 단일 공백으로 구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-327">Each parameter name should be delimited with a single space.</span></span>
- <span data-ttu-id="85a7d-328">이 기능은 cache-key에서 쿼리 문자열 매개 변수를 포함할지 또는 제외할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-328">This feature determines whether query string parameters will be included or excluded from the cache-key.</span></span> <span data-ttu-id="85a7d-329">각 옵션에 제공되는 추가 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-329">Additional information is provided for each option below.</span></span>

<span data-ttu-id="85a7d-330">형식</span><span class="sxs-lookup"><span data-stu-id="85a7d-330">Type</span></span>|<span data-ttu-id="85a7d-331">설명</span><span class="sxs-lookup"><span data-stu-id="85a7d-331">Description</span></span>
--|--
 <span data-ttu-id="85a7d-332">포함</span><span class="sxs-lookup"><span data-stu-id="85a7d-332">Include</span></span>|  <span data-ttu-id="85a7d-333">지정된 매개 변수마다 cache-key에 포함되어야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-333">Indicates that each specified parameter should be included in the cache-key.</span></span> <span data-ttu-id="85a7d-334">이 기능에 정의된 쿼리 문자열 매개 변수의 고유한 값을 포함하는 요청마다 고유한 cache-key가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-334">A unique cache-key will be generated for each request that contains a unique value for a query string parameter defined in this feature.</span></span> 
 <span data-ttu-id="85a7d-335">모두 포함</span><span class="sxs-lookup"><span data-stu-id="85a7d-335">Include All</span></span>  |<span data-ttu-id="85a7d-336">고유한 쿼리 문자열을 포함하는 자산에 대한 요청마다 고유한 cache-key가 생성됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-336">Indicates that a unique cache-key will be created for each request to an asset that includes a unique query string.</span></span> <span data-ttu-id="85a7d-337">이러한 유형의 구성은 일반적으로 캐시 적중률이 낮을 수 있으므로 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-337">This type of configuration is not typically recommended since it may lead to a small percentage of cache hits.</span></span> <span data-ttu-id="85a7d-338">이 경우 요청을 더 많이 처리해야 하기 때문에 원본 서버의 부하를 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-338">This will increase the load on the origin server, since it will have to serve more requests.</span></span> <span data-ttu-id="85a7d-339">이 구성은 Query-String Caching 페이지에서 "unique-cache"로 알려진 캐싱 동작을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-339">This configuration duplicates the caching behavior known as "unique-cache" on the Query-String Caching page.</span></span> 
 <span data-ttu-id="85a7d-340">제외</span><span class="sxs-lookup"><span data-stu-id="85a7d-340">Exclude</span></span> | <span data-ttu-id="85a7d-341">지정된 매개 변수만 cache-key에서 제외됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-341">Indicates that only the specified parameter(s) will be excluded from the cache-key.</span></span> <span data-ttu-id="85a7d-342">다른 모든 쿼리 문자열 매개 변수는 cache-key에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-342">All other query string parameters will be included in the cache-key.</span></span> 
 <span data-ttu-id="85a7d-343">모두 제외</span><span class="sxs-lookup"><span data-stu-id="85a7d-343">Exclude All</span></span>  |<span data-ttu-id="85a7d-344">모든 쿼리 문자열 매개 변수가 cache-key에서 제외됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-344">Indicates that all query string parameters will be excluded from the cache-key.</span></span> <span data-ttu-id="85a7d-345">이 구성은 Query-String Caching 페이지에서 "standard-cache"로 알려진 기본 캐싱 동작을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-345">This configuration duplicates the default caching behavior, which is known as "standard-cache" on the Query-String Caching page.</span></span> 

<span data-ttu-id="85a7d-346">HTTP 규칙 엔진의 강력한 기능을 사용하면 쿼리 문자열 캐싱을 구현하는 방식을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-346">The power of HTTP Rules Engine allows you to customize the manner in which query string caching is implemented.</span></span> <span data-ttu-id="85a7d-347">예를 들어 특정 위치 또는 파일 형식에서만 쿼리 문자열 캐싱을 수행하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-347">For example, you can specify that query string caching only be performed on certain locations or file types.</span></span>

<span data-ttu-id="85a7d-348">Query-String Caching 페이지에서 "no-cache"로 알려진 쿼리 문자열 캐싱 동작을 복제하려면 URL 쿼리 와일드카드 일치 조건과 Bypass-Cache 기능을 포함한 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-348">If you would like to duplicate the query string caching behavior known as "no-cache" on the Query-String Caching page, then you will need to create a rule that contains a URL Query Wildcard match condition and a Bypass Cache feature.</span></span> <span data-ttu-id="85a7d-349">URL 쿼리 와일드카드 일치 조건은 별표(*)로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-349">The URL Query Wildcard match condition should be set to an asterisk (*).</span></span>

#### <a name="sample-scenarios"></a><span data-ttu-id="85a7d-350">샘플 시나리오</span><span class="sxs-lookup"><span data-stu-id="85a7d-350">Sample Scenarios</span></span>

<span data-ttu-id="85a7d-351">이 기능의 샘플 사용법이 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-351">Sample usage for this feature is provided below.</span></span> <span data-ttu-id="85a7d-352">제공되는 샘플 요청과 기본 cache-key는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-352">A sample request and the default cache-key are provided below.</span></span>

- <span data-ttu-id="85a7d-353">**샘플 요청:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01</span><span class="sxs-lookup"><span data-stu-id="85a7d-353">**Sample request:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01</span></span>
- <span data-ttu-id="85a7d-354">**기본 cache-key:** /800001/Origin/folder/asset.htm</span><span class="sxs-lookup"><span data-stu-id="85a7d-354">**Default cache-key:** /800001/Origin/folder/asset.htm</span></span>

##### <a name="include"></a><span data-ttu-id="85a7d-355">포함</span><span class="sxs-lookup"><span data-stu-id="85a7d-355">Include</span></span>

<span data-ttu-id="85a7d-356">샘플 구성:</span><span class="sxs-lookup"><span data-stu-id="85a7d-356">Sample configuration:</span></span>

- <span data-ttu-id="85a7d-357">**형식:** 포함</span><span class="sxs-lookup"><span data-stu-id="85a7d-357">**Type:** Include</span></span>
- <span data-ttu-id="85a7d-358">**매개 변수:** language</span><span class="sxs-lookup"><span data-stu-id="85a7d-358">**Parameter(s):** language</span></span>

<span data-ttu-id="85a7d-359">이러한 유형의 구성은 다음과 같은 cache-key 쿼리 문자열 매개 변수를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-359">This type of configuration would generate the following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a><span data-ttu-id="85a7d-360">모두 포함</span><span class="sxs-lookup"><span data-stu-id="85a7d-360">Include All</span></span>

<span data-ttu-id="85a7d-361">샘플 구성:</span><span class="sxs-lookup"><span data-stu-id="85a7d-361">Sample configuration:</span></span>

- <span data-ttu-id="85a7d-362">**형식:** 모두 포함</span><span class="sxs-lookup"><span data-stu-id="85a7d-362">**Type:** Include All</span></span>

<span data-ttu-id="85a7d-363">이러한 유형의 구성은 다음과 같은 cache-key 쿼리 문자열 매개 변수를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-363">This type of configuration would generate the following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a><span data-ttu-id="85a7d-364">제외</span><span class="sxs-lookup"><span data-stu-id="85a7d-364">Exclude</span></span>

<span data-ttu-id="85a7d-365">샘플 구성:</span><span class="sxs-lookup"><span data-stu-id="85a7d-365">Sample configuration:</span></span>

- <span data-ttu-id="85a7d-366">**형식:** 제외</span><span class="sxs-lookup"><span data-stu-id="85a7d-366">**Type:** Exclude</span></span>
- <span data-ttu-id="85a7d-367">**매개 변수:** sessionid userid</span><span class="sxs-lookup"><span data-stu-id="85a7d-367">**Parameter(s):** sessionid userid</span></span>

<span data-ttu-id="85a7d-368">이러한 유형의 구성은 다음과 같은 cache-key 쿼리 문자열 매개 변수를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-368">This type of configuration would generate the following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a><span data-ttu-id="85a7d-369">모두 제외</span><span class="sxs-lookup"><span data-stu-id="85a7d-369">Exclude All</span></span>

<span data-ttu-id="85a7d-370">샘플 구성:</span><span class="sxs-lookup"><span data-stu-id="85a7d-370">Sample configuration:</span></span>

- <span data-ttu-id="85a7d-371">**형식:** 모두 제외</span><span class="sxs-lookup"><span data-stu-id="85a7d-371">**Type:** Exclude All</span></span>

<span data-ttu-id="85a7d-372">이러한 유형의 구성은 다음과 같은 cache-key 쿼리 문자열 매개 변수를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-372">This type of configuration would generate the following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a><span data-ttu-id="85a7d-373">Cache-Key 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-373">Cache-Key Rewrite</span></span>
<span data-ttu-id="85a7d-374">**목적:** 요청과 관련된 cache-key를 다시 씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-374">**Purpose:** Rewrites the cache-key associated with a request.</span></span>

<span data-ttu-id="85a7d-375">cache-key는 캐싱을 위해 자산을 식별하는 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-375">A cache-key is the relative path that identifies an asset for the purposes of caching.</span></span> <span data-ttu-id="85a7d-376">즉 서버에서 cache-key에 정의된 경로에 따라 자산의 캐시된 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-376">In other words, our servers will check for a cached version of an asset according to its path as defined by its cache-key.</span></span>

<span data-ttu-id="85a7d-377">다음 두 옵션을 모두 정의하여 이 기능을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-377">Configure this feature by defining both of the following options:</span></span>

<span data-ttu-id="85a7d-378">옵션</span><span class="sxs-lookup"><span data-stu-id="85a7d-378">Option</span></span>|<span data-ttu-id="85a7d-379">설명</span><span class="sxs-lookup"><span data-stu-id="85a7d-379">Description</span></span>
--|--
<span data-ttu-id="85a7d-380">원래 경로</span><span class="sxs-lookup"><span data-stu-id="85a7d-380">Original Path</span></span>| <span data-ttu-id="85a7d-381">cache-key를 다시 쓰는 요청의 형식에 대한 상대 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-381">Define the relative path to the types of requests whose cache-key will be rewritten.</span></span> <span data-ttu-id="85a7d-382">상대 경로는 기본 경로를 선택한 다음 정규식 패턴을 정의함으로써 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-382">A relative path can be defined by selecting a base origin path and then defining a regular expression pattern.</span></span>
<span data-ttu-id="85a7d-383">새 경로</span><span class="sxs-lookup"><span data-stu-id="85a7d-383">New Path</span></span>|<span data-ttu-id="85a7d-384">새 cache-key에 대한 상대 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-384">Define the relative path for the new cache-key.</span></span> <span data-ttu-id="85a7d-385">상대 경로는 기본 경로를 선택한 다음 정규식 패턴을 정의함으로써 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-385">A relative path can be defined by selecting a base origin path and then defining a regular expression pattern.</span></span> <span data-ttu-id="85a7d-386">이 상대 경로는 HTTP 변수를 사용하여 동적으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-386">This relative path can be dynamically constructed through the use of HTTP variables</span></span>
<span data-ttu-id="85a7d-387">**기본 동작:** 요청의 cache-key는 요청 URI에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-387">**Default Behavior:** A request's cache-key is determined by the request URI.</span></span>

###<a name="complete-cache-fill"></a><span data-ttu-id="85a7d-388">전체 캐시 채우기</span><span class="sxs-lookup"><span data-stu-id="85a7d-388">Complete Cache Fill</span></span>
<span data-ttu-id="85a7d-389">**목적:** 요청으로 인해 에지 서버에서 부분 캐시가 누락된 경우 수행할 작업을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-389">**Purpose:** Determines what happens when a request results in a partial cache miss on an edge server.</span></span>

<span data-ttu-id="85a7d-390">부분 캐시 누락은 에지 서버에 완전히 다운로드되지 않은 자산의 캐시 상태를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-390">A partial cache miss describes the cache status for an asset that was not completely downloaded to an edge server.</span></span> <span data-ttu-id="85a7d-391">자산을 에지 서버에 부분적으로만 캐시한 경우 해당 자산에 대한 다음 요청이 원본 서버로 다시 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-391">If an asset is only partially cached on an edge server, then the next request for that asset will be forwarded again to the origin server.</span></span>
<!---
This feature is not available for the ADN platform. The typical traffic on this platform consists of relatively small assets. The size of the assets served through these platforms helps mitigate the effects of partial cache misses, since the next request will typically result in the asset being cached on that POP.
--->
<span data-ttu-id="85a7d-392">부분 캐시 누락은 일반적으로 사용자가 다운로드를 중단한 후에 발생하거나 HTTP 범위 요청을 사용하여 단독으로 요청된 자산에 대해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-392">A partial cache miss typically occurs after a user aborts a download or for assets that are solely requested using HTTP range requests.</span></span> <span data-ttu-id="85a7d-393">이 기능은 일반적으로 사용자가 처음부터 끝까지 다운로드하지 않는 대규모 자산(예: 비디오)에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-393">This feature is most useful for large assets where users will not typically download them from start to finish (e.g., videos).</span></span> <span data-ttu-id="85a7d-394">따라서 이 기능은 기본적으로 HTTP Large 플랫폼에서 사용하도록 설정되며,</span><span class="sxs-lookup"><span data-stu-id="85a7d-394">As a result, this feature is enabled by default on the HTTP Large platform.</span></span> <span data-ttu-id="85a7d-395">다른 모든 플랫폼에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-395">It is disabled on all other platforms.</span></span>

<span data-ttu-id="85a7d-396">고객 원본 서버의 부하를 줄이고 고객이 콘텐츠를 다운로드하는 속도를 높이므로 HTTP Large 플랫폼의 기본 구성을 그대로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-396">It is recommended to leave the default configuration for the HTTP Large platform, since it will reduce the load on your customer origin server and increase the speed at which your customers download your content.</span></span>

<span data-ttu-id="85a7d-397">캐시 설정을 추적하는 방식 때문에 이 기능을 에지 Cname, 요청 헤더 리터럴, 요청 헤더 와일드카드, URL 쿼리 리터럴 및 URL 쿼리 와일드카드와 같은 일치 조건과 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-397">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following Match conditions: Edge Cname, Request Header Literal, Request Header Wildcard, URL Query Literal, and URL Query Wildcard.</span></span>

<span data-ttu-id="85a7d-398">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-398">Value</span></span>|<span data-ttu-id="85a7d-399">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-399">Result</span></span>
--|--
<span data-ttu-id="85a7d-400">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-400">Enabled</span></span>|<span data-ttu-id="85a7d-401">기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-401">Restores the default behavior.</span></span> <span data-ttu-id="85a7d-402">기본 동작은 에지 서버에서 원본 서버에 있는 자산의 백그라운드 페치를 시작하도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-402">The default behavior is to force the edge server to initiate a background fetch of the asset from the origin server.</span></span> <span data-ttu-id="85a7d-403">그런 다음 자산이 에지 서버의 로컬 캐시에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-403">After which, the asset will be in the edge server's local cache.</span></span>
<span data-ttu-id="85a7d-404">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-404">Disabled</span></span>|<span data-ttu-id="85a7d-405">에지 서버에서 자산에 대한 백그라운드 페치를 수행하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-405">Prevents an edge server from performing a background fetch for the asset.</span></span> <span data-ttu-id="85a7d-406">즉 해당 지역의 해당 자산에 대한 다음 요청으로 인해 에지 서버에서 고객 원본 서버의 해당 자산을 요청하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-406">This means that the next request for that asset from that region will cause an edge server to request it from the customer origin server.</span></span>

<span data-ttu-id="85a7d-407">**기본 동작**: 사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-407">**Default Behavior:** Enabled.</span></span>

###<a name="compress-file-types"></a><span data-ttu-id="85a7d-408">압축 파일 형식</span><span class="sxs-lookup"><span data-stu-id="85a7d-408">Compress File Types</span></span>
<span data-ttu-id="85a7d-409">**목적:** 서버에서 압축할 파일 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-409">**Purpose:** Defines the file formats that will be compressed on the server.</span></span>

<span data-ttu-id="85a7d-410">파일 형식은 인터넷 미디어 유형, 즉 Content-Type을 사용하여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-410">A file format can be specified using its Internet media type (i.e., Content-Type).</span></span> <span data-ttu-id="85a7d-411">인터넷 미디어 유형은 서버에서 특정 자산의 파일 형식을 식별할 수 있는 플랫폼 독립적 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-411">Internet media type is platform-independent metadata that allows our servers to identify the file format of a particular asset.</span></span> <span data-ttu-id="85a7d-412">일반적인 인터넷 미디어 유형 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-412">A list of common Internet media types is provided below.</span></span>

<span data-ttu-id="85a7d-413">인터넷 미디어 유형</span><span class="sxs-lookup"><span data-stu-id="85a7d-413">Internet Media Type</span></span>|<span data-ttu-id="85a7d-414">설명</span><span class="sxs-lookup"><span data-stu-id="85a7d-414">Description</span></span>
--|--
<span data-ttu-id="85a7d-415">텍스트/일반</span><span class="sxs-lookup"><span data-stu-id="85a7d-415">text/plain</span></span>|<span data-ttu-id="85a7d-416">일반 텍스트 파일</span><span class="sxs-lookup"><span data-stu-id="85a7d-416">Plain text files</span></span>
<span data-ttu-id="85a7d-417">텍스트/html</span><span class="sxs-lookup"><span data-stu-id="85a7d-417">text/html</span></span>| <span data-ttu-id="85a7d-418">HTML 파일</span><span class="sxs-lookup"><span data-stu-id="85a7d-418">HTML files</span></span>
<span data-ttu-id="85a7d-419">텍스트/css</span><span class="sxs-lookup"><span data-stu-id="85a7d-419">text/css</span></span>|<span data-ttu-id="85a7d-420">CSS(스타일시트)</span><span class="sxs-lookup"><span data-stu-id="85a7d-420">Cascading Style Sheets (CSS)</span></span>
<span data-ttu-id="85a7d-421">application/x-javascript</span><span class="sxs-lookup"><span data-stu-id="85a7d-421">application/x-javascript</span></span>|<span data-ttu-id="85a7d-422">JavaScript</span><span class="sxs-lookup"><span data-stu-id="85a7d-422">Javascript</span></span>
<span data-ttu-id="85a7d-423">application/javascript</span><span class="sxs-lookup"><span data-stu-id="85a7d-423">application/javascript</span></span>|<span data-ttu-id="85a7d-424">JavaScript</span><span class="sxs-lookup"><span data-stu-id="85a7d-424">Javascript</span></span>
<span data-ttu-id="85a7d-425">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-425">Key information:</span></span>

- <span data-ttu-id="85a7d-426">각각 하나의 공백으로 구분하여 여러 인터넷 미디어 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-426">Specify multiple Internet media types by delimiting each one with a single space.</span></span> 
- <span data-ttu-id="85a7d-427">이 기능은 1MB 미만 크기의 자산만 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-427">This feature will only compress assets whose size is less than 1 MB.</span></span> <span data-ttu-id="85a7d-428">더 큰 자산은 서버에서 압축하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-428">Larger assets will not be compressed by our servers.</span></span>
- <span data-ttu-id="85a7d-429">이미지, 비디오 및 오디오 미디어 자산(예: JPG, MP3, MP4 등)과 같은 특정 유형의 콘텐츠는 이미 압축되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-429">Certain types of content, such as images, video, and audio media assets (e.g., JPG, MP3, MP4, etc.), are already compressed.</span></span> <span data-ttu-id="85a7d-430">이러한 유형의 자산을 추가로 압축해도 파일 크기가 크게 줄어들지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-430">Additional compression on these types of assets will not significantly diminish file size.</span></span> <span data-ttu-id="85a7d-431">따라서 이러한 유형의 자산에는 압축을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-431">Therefore, it is recommended that you do not enable compression on these types of assets.</span></span>
- <span data-ttu-id="85a7d-432">별표와 같은 와일드카드 문자는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-432">Wildcard characters, such as asterisks, are not supported.</span></span>
- <span data-ttu-id="85a7d-433">이 기능을 규칙에 추가하기 전에 이 규칙이 적용될 플랫폼의 Compression 페이지에서 압축 사용 안 함 옵션을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-433">Before adding this feature to a rule, make sure to set the Compression Disabled option on the Compression page for the platform to which this rule will be applied.</span></span>

###<a name="default-internal-max-age"></a><span data-ttu-id="85a7d-434">기본 내부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="85a7d-434">Default Internal Max-Age</span></span>
<span data-ttu-id="85a7d-435">**목적:** 에지 서버에서 원본 서버 캐시 유효성 재검사를 위한 기본 max-age 간격을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-435">**Purpose:** Determines the default max-age interval for edge server to origin server cache revalidation.</span></span> <span data-ttu-id="85a7d-436">즉 에지 서버에서 캐시된 자산이 원본 서버에 저장된 자산과 일치하는지 여부를 확인할 때까지 경과할 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-436">In other words, the amount of time that will pass before an edge server will check whether a cached asset matches the asset stored on the origin server.</span></span>

<span data-ttu-id="85a7d-437">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-437">Key information:</span></span>

- <span data-ttu-id="85a7d-438">이 작업은 Cache-Control 또는 Expires 헤더에 max-age 표시를 할당하지 않은 원본 서버의 응답에 대해서만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-438">This action will only take place for responses from an origin server that did not assign a max-age indication in the Cache-Control or Expires header.</span></span>
- <span data-ttu-id="85a7d-439">이 작업은 캐시 가능하다고 간주되지 않는 자산에 대해서는 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-439">This action will not take place for assets that are not deemed cacheable.</span></span>
- <span data-ttu-id="85a7d-440">이 작업은 브라우저-에지 서버 캐시 유효성 재검사에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-440">This action does not affect browser to edge server cache revalidations.</span></span> <span data-ttu-id="85a7d-441">이러한 유형의 유효성 재검사는 외부 Max-Age 기능으로 사용자 지정할 수 있는 브라우저로 보낸 Cache-Control 또는 Expires 헤더에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-441">These types of revalidations are determined by the Cache-Control or Expires headers sent to the browser, which can be customized with the External Max-Age feature.</span></span>
- <span data-ttu-id="85a7d-442">이 작업의 결과는 응답 헤더와 콘텐츠의 에지 서버에서 반환된 콘텐츠에 대해 관찰 가능한 영향을 주지 않지만, 에지 서버에서 원본 서버로 보내는 유효성 검사 트래픽의 양에는 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-442">The results of this action do not have an observable effect on the response headers and the content returned from edge servers for your content, but it may have an effect on the amount of revalidation traffic sent from edge servers to your origin server.</span></span>
- <span data-ttu-id="85a7d-443">이 기능은 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-443">Configure this feature by:</span></span>
    - <span data-ttu-id="85a7d-444">기본 내부 max-age 간격을 적용할 수 있는 상태 코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-444">Selecting the status code for which a default internal max-age can be applied.</span></span>
    - <span data-ttu-id="85a7d-445">정수 값을 지정한 다음 원하는 시간 단위(즉 초, 분, 시간 등)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-445">Specifying an integer value and then selecting the desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="85a7d-446">이 값은 기본 내부 max-age 간격을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-446">This value defines the default internal max-age interval.</span></span>

- <span data-ttu-id="85a7d-447">시간 단위를 "끄기"로 설정하면 Cache-Control 또는 Expires 헤더에 max-age 표시를 할당하지 않은 요청에 대해 기본 내부 max-age 간격을 7일로 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-447">Setting the time unit to "Off" will assign a default internal max-age interval of 7 days for requests that have not been assigned a max-age indication in their Cache-Control or Expires header.</span></span>
- <span data-ttu-id="85a7d-448">캐시 설정을 추적하는 방식으로 인해 이 기능은 다음 일치 조건과 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-448">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following match conditions:</span></span> 
    - <span data-ttu-id="85a7d-449">에지</span><span class="sxs-lookup"><span data-stu-id="85a7d-449">Edge</span></span> 
    - <span data-ttu-id="85a7d-450">Cname</span><span class="sxs-lookup"><span data-stu-id="85a7d-450">Cname</span></span>
    - <span data-ttu-id="85a7d-451">요청 헤더 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-451">Request Header Literal</span></span>
    - <span data-ttu-id="85a7d-452">요청 헤더 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-452">Request Header Wildcard</span></span>
    - <span data-ttu-id="85a7d-453">요청 메서드</span><span class="sxs-lookup"><span data-stu-id="85a7d-453">Request Method</span></span>
    - <span data-ttu-id="85a7d-454">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-454">URL Query Literal</span></span>
    - <span data-ttu-id="85a7d-455">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-455">URL Query Wildcard</span></span>

<span data-ttu-id="85a7d-456">**기본값:** 7일</span><span class="sxs-lookup"><span data-stu-id="85a7d-456">**Default Value:** 7 days</span></span>

###<a name="expires-header-treatment"></a><span data-ttu-id="85a7d-457">만료 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="85a7d-457">Expires Header Treatment</span></span>
<span data-ttu-id="85a7d-458">**목적:** 외부 Max-Age 기능이 활성 상태일 때 에지 서버의 Expires 헤더 생성을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-458">**Purpose:** Controls the generation of Expires headers by an edge server when the External Max-Age feature is active.</span></span>

<span data-ttu-id="85a7d-459">이 유형의 구성을 획득하는 가장 쉬운 방법은 동일한 문에 외부 Max-Age와 Expires 헤더 처리 기능을 배치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-459">The easiest way to achieve this type of configuration is to place the External Max-Age and the Expires Header Treatment features in the same statement.</span></span>

<span data-ttu-id="85a7d-460">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-460">Value</span></span>|<span data-ttu-id="85a7d-461">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-461">Result</span></span>
--|--
<span data-ttu-id="85a7d-462">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-462">Overwrite</span></span>|<span data-ttu-id="85a7d-463">다음과 같은 작업이 수행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-463">Ensures that the following actions will take place:</span></span><br/><span data-ttu-id="85a7d-464">- 원본 서버에서 생성한 Expires 헤더를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-464">- Overwrites the Expires header generated by the origin server.</span></span><br/><span data-ttu-id="85a7d-465">- 외부 Max-Age 기능으로 생성한 Expires 헤더를 응답에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-465">- Adds the Expires header produced by the External Max-Age feature to the response.</span></span>
<span data-ttu-id="85a7d-466">통과</span><span class="sxs-lookup"><span data-stu-id="85a7d-466">Pass Through</span></span>|<span data-ttu-id="85a7d-467">외부 Max-Age 기능으로 생성한 Expires 헤더를 응답에 절대 추가하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-467">Ensures that the Expires header produced by the External Max-Age feature is never added to the response.</span></span> <br/> <span data-ttu-id="85a7d-468">원본 서버에서 Expires 헤더를 생성하는 경우 최종 사용자에게 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-468">If the origin server produces an Expires header, it will pass through to the end-user.</span></span> <br/><span data-ttu-id="85a7d-469">원본 서버에서 Expires 헤더를 생성하지 않은 경우 이 옵션은 응답 헤더에 Expires 헤더를 포함하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-469">If the origin server does not produce an Expires header, then this option may cause the response header to not contain an Expires header.</span></span>
<span data-ttu-id="85a7d-470">없는 경우 추가</span><span class="sxs-lookup"><span data-stu-id="85a7d-470">Add if Missing</span></span>| <span data-ttu-id="85a7d-471">Expires 헤더를 원본 서버로부터 수신하지 않은 경우 이 옵션은 외부 Max-Age 기능으로 생성한 Expires 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-471">If an Expires header was not received from the origin server, then this option adds the Expires header produced by the External Max-Age feature.</span></span> <span data-ttu-id="85a7d-472">이 옵션은 모든 자산에 Expires 헤더를 할당하도록 하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-472">This option is useful for ensuring that all assets will be assigned an Expires header.</span></span>
<span data-ttu-id="85a7d-473">제거</span><span class="sxs-lookup"><span data-stu-id="85a7d-473">Remove</span></span>| <span data-ttu-id="85a7d-474">헤더 응답에 Expires 헤더를 포함하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-474">Ensures that an Expires header is not included with the header response.</span></span> <span data-ttu-id="85a7d-475">Expires 헤더를 이미 할당한 경우 헤더 응답에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-475">If an Expires header has already been assigned, then it will be stripped from the header response.</span></span>

<span data-ttu-id="85a7d-476">**기본 동작:** 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-476">**Default Behavior:** Overwrite</span></span>

###<a name="external-max-age"></a><span data-ttu-id="85a7d-477">외부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="85a7d-477">External Max-Age</span></span>
<span data-ttu-id="85a7d-478">**목적:** 브라우저에서 에지 서버 캐시 유효성 재검사를 위한 max-age 간격을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-478">**Purpose:** Determines the max-age interval for browser to edge server cache revalidation.</span></span> <span data-ttu-id="85a7d-479">즉 브라우저에서 에지 서버에 있는 새 버전의 자산을 확인할 수 있을 때까지 경과할 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-479">In other words, the amount of time that will pass before a browser can check for a new version of an asset from an edge server.</span></span>

<span data-ttu-id="85a7d-480">이 기능을 사용하면 에지 서버에서 Cache-Control:max-age 및 Expires 헤더를 생성하고 HTTP 클라이언트로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-480">Enabling this feature will generate Cache-Control:max-age and Expires headers from our edge servers and send them to the HTTP client.</span></span> <span data-ttu-id="85a7d-481">기본적으로 이러한 헤더는 원본 서버에서 만든 헤더를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-481">By default, these headers will overwrite those created by the origin server.</span></span> <span data-ttu-id="85a7d-482">그러나 Cache-Control 헤더 처리 및 Expires 헤더 처리 기능을 사용하여 이 동작을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-482">However, the Cache-Control Header Treatment and the Expires Header Treatment features may be used to alter this behavior.</span></span>

<span data-ttu-id="85a7d-483">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-483">Key information:</span></span>

- <span data-ttu-id="85a7d-484">이 작업은 에지 서버-원본 서버 캐시 유효성 재검사에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-484">This action does not affect edge server to origin server cache revalidations.</span></span> <span data-ttu-id="85a7d-485">이러한 유형의 유효성 재검사는 원본 서버에서 받은 Cache-Control/Expires 헤더에 의해 결정되며, 기본 내부 Max-Age 및 강제 내부 Max-Age 기능을 사용하여 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-485">These types of revalidations are determined by the Cache-Control/Expires headers received from the origin server, and can be customized with the Default Internal Max-Age and the Force Internal Max-Age features.</span></span>
- <span data-ttu-id="85a7d-486">정수 값을 지정한 다음 원하는 시간 단위(즉 초, 분, 시간 등)를 선택하여 이 기능을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-486">Configure this feature by specifying an integer value and selecting the desired time unit (i.e., seconds, minutes, hours, etc.).</span></span>
- <span data-ttu-id="85a7d-487">이 기능을 음수 값으로 설정하면 에지 서버에서 브라우저에 대한 각 응답과 함께 과거에 설정된 Cache-Control:no-cache 및 Expires 시간을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-487">Setting this feature to a negative value causes our edge servers to send a Cache-Control:no-cache and an Expires time that is set in the past with each response to the browser.</span></span> <span data-ttu-id="85a7d-488">HTTP 클라이언트에서 응답을 캐시하지 않지만 이 설정은 원본 서버에서 응답을 캐시하는 에지 서버의 기능에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-488">Although an HTTP client will not cache the response, this setting will not affect our edge servers' ability to cache the response from the origin server.</span></span>
- <span data-ttu-id="85a7d-489">시간 단위를 "끄기"로 설정하면 이 기능을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-489">Setting the time unit to "Off" will disable this feature.</span></span> <span data-ttu-id="85a7d-490">원본 서버의 응답으로 캐시된 Cache-Control/Expires 헤더는 브라우저로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-490">The Cache-Control/Expires headers cached with the response of the origin server will pass through to the browser.</span></span>

<span data-ttu-id="85a7d-491">**기본 동작:** 끄기</span><span class="sxs-lookup"><span data-stu-id="85a7d-491">**Default Behavior:** Off</span></span>

###<a name="force-internal-max-age"></a><span data-ttu-id="85a7d-492">강제 내부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="85a7d-492">Force Internal Max-Age</span></span>
<span data-ttu-id="85a7d-493">**목적:** 에지 서버에서 원본 서버 캐시 유효성 재검사를 위한 max-age 간격을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-493">**Purpose:** Determines the max-age interval for edge server to origin server cache revalidation.</span></span> <span data-ttu-id="85a7d-494">즉 에지 서버에서 캐시된 자산이 원본 서버에 저장된 자산과 일치하는지 여부를 확인할 수 있을 때까지 경과할 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-494">In other words, the amount of time that will pass before an edge server can check whether a cached asset matches the asset stored on the origin server.</span></span>

<span data-ttu-id="85a7d-495">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-495">Key information:</span></span>

- <span data-ttu-id="85a7d-496">이 기능은 원본 서버로부터 생성한 Cache-Control 또는 Expires 헤더에 정의된 max-age 간격을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-496">This feature will override the max-age interval defined in Cache-Control or Expires headers generated from an origin server.</span></span>
- <span data-ttu-id="85a7d-497">이 기능은 브라우저-에지 서버 캐시 유효성 재검사에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-497">This feature does not affect browser to edge server cache revalidations.</span></span> <span data-ttu-id="85a7d-498">이러한 유형의 유효성 재검사는 브라우저로 보낸 Cache-Control 또는 Expires 헤더에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-498">These types of revalidations are determined by the Cache-Control or Expires headers sent to the browser.</span></span>
- <span data-ttu-id="85a7d-499">이 기능은 에지 서버에서 요청자에게 전달한 응답에 관찰 가능한 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-499">This feature does not have an observable effect on the response delivered by an edge server to the requester.</span></span> <span data-ttu-id="85a7d-500">그러나 에지 서버에서 원본 서버로 보낸 유효성 재검사 트래픽의 양에 영향을 중 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-500">However, it may have an effect on the amount of revalidation traffic sent from our edge servers to the origin server.</span></span>
- <span data-ttu-id="85a7d-501">이 기능은 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-501">Configure this feature by:</span></span>
    - <span data-ttu-id="85a7d-502">내부 max-age 간격을 적용할 상태 코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-502">Selecting the status code for which an internal max-age will be applied.</span></span>
    - <span data-ttu-id="85a7d-503">정수 값을 지정하고 원하는 시간 단위(즉 초, 분, 시간 등)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-503">Specifying an integer value and selecting the desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="85a7d-504">이 값은 요청의 max-age 간격을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-504">This value defines the request's max-age interval.</span></span>

- <span data-ttu-id="85a7d-505">시간 단위를 "끄기"로 설정하면 이 기능을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-505">Setting the time unit to "Off" disables this feature.</span></span> <span data-ttu-id="85a7d-506">내부 max-age 간격은 요청된 자산에 할당되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-506">An internal max-age interval will not be assigned to requested assets.</span></span> <span data-ttu-id="85a7d-507">원래 헤더에 캐싱 지침이 없으면 기본 내부 Max-Age 기능의 활성 설정에 따라 자산이 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-507">If the original header does not contain caching instructions, then the asset will be cached according to the active setting in the Default Internal Max-Age feature.</span></span>
- <span data-ttu-id="85a7d-508">캐시 설정을 추적하는 방식으로 인해 이 기능은 다음 일치 조건과 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-508">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following match conditions:</span></span> 
    - <span data-ttu-id="85a7d-509">에지</span><span class="sxs-lookup"><span data-stu-id="85a7d-509">Edge</span></span> 
    - <span data-ttu-id="85a7d-510">Cname</span><span class="sxs-lookup"><span data-stu-id="85a7d-510">Cname</span></span>
    - <span data-ttu-id="85a7d-511">요청 헤더 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-511">Request Header Literal</span></span>
    - <span data-ttu-id="85a7d-512">요청 헤더 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-512">Request Header Wildcard</span></span>
    - <span data-ttu-id="85a7d-513">요청 메서드</span><span class="sxs-lookup"><span data-stu-id="85a7d-513">Request Method</span></span>
    - <span data-ttu-id="85a7d-514">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-514">URL Query Literal</span></span>
    - <span data-ttu-id="85a7d-515">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-515">URL Query Wildcard</span></span>

<span data-ttu-id="85a7d-516">**기본 동작:** 끄기</span><span class="sxs-lookup"><span data-stu-id="85a7d-516">**Default Behavior:** Off</span></span>

###<a name="h264-support-http-progressive-download"></a><span data-ttu-id="85a7d-517">H.264 지원(HTTP 점진적 다운로드)</span><span class="sxs-lookup"><span data-stu-id="85a7d-517">H.264 Support (HTTP Progressive Download)</span></span>
<span data-ttu-id="85a7d-518">**목적:** 콘텐츠를 스트리밍하는 데 사용할 수 있는 H.264 파일 형식의 유형을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-518">**Purpose:** Determines the types of H.264 file formats that may be used to stream content.</span></span>

<span data-ttu-id="85a7d-519">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-519">Key information:</span></span>

- <span data-ttu-id="85a7d-520">파일 확장명 옵션에서 허용되는 H.264 파일 이름 확장명의 공백으로 구분된 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-520">Define a space-delimited set of allowed H.264 filename extensions in the File Extensions option.</span></span> <span data-ttu-id="85a7d-521">파일 확장명 옵션은 기본 동작을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-521">The File Extensions option will override the default behavior.</span></span> <span data-ttu-id="85a7d-522">이 옵션을 설정할 때 파일 이름 확장명을 포함하여 MP4 및 F4V 지원을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-522">Maintain MP4 and F4V support by including those filename extensions when setting this option.</span></span> 
- <span data-ttu-id="85a7d-523">각 파일 이름 확장명을 지정할 때는 마침표를 포함해야 합니다(예: .mp4 .f4v).</span><span class="sxs-lookup"><span data-stu-id="85a7d-523">Make sure to include a period when specifying each filename extension (e.g., .mp4 .f4v).</span></span>

<span data-ttu-id="85a7d-524">**기본 동작:** HTTP 점진적 다운로드는 기본적으로 MP4 및 F4V 미디어를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-524">**Default Behavior:** HTTP Progressive Download supports MP4 and F4V media by default.</span></span>

###<a name="honor-no-cache-request"></a><span data-ttu-id="85a7d-525">no-cache 요청 부여</span><span class="sxs-lookup"><span data-stu-id="85a7d-525">Honor no-cache request</span></span>
<span data-ttu-id="85a7d-526">**목적:** HTTP 클라이언트의 no-cache 요청을 원본 서버에 전달할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-526">**Purpose:** Determines whether an HTTP client's no-cache requests will be forwarded to the origin server.</span></span>

<span data-ttu-id="85a7d-527">no-cache 요청은 HTTP 클라이언트에서 HTTP 요청에 Cache-Control:no-cache 및/또는 Pragma:no-cache 헤더를 보낼 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-527">A no-cache request occurs when the HTTP client sends a Cache-Control:no-cache and/or Pragma:no-cache header in the HTTP request.</span></span>

<span data-ttu-id="85a7d-528">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-528">Value</span></span>|<span data-ttu-id="85a7d-529">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-529">Result</span></span>
--|--
<span data-ttu-id="85a7d-530">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-530">Enabled</span></span>|<span data-ttu-id="85a7d-531">HTTP 클라이언트의 no-cache 요청을 원본 서버로 전달할 수 있으며, 원본 서버에서 에지 서버를 통해 응답 헤더와 본문을 HTTP 클라이언트에 다시 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-531">Allows an HTTP client's no-cache requests to be forwarded to the origin server, and the origin server will return the response headers and the body through the edge server back to the HTTP client.</span></span>
<span data-ttu-id="85a7d-532">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-532">Disabled</span></span>|<span data-ttu-id="85a7d-533">기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-533">Restores the default behavior.</span></span> <span data-ttu-id="85a7d-534">기본 동작은 no-cache 요청을 원본 서버로 전달하지 않도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-534">The default behavior is to prevent no-cache requests from being forwarded to the origin server.</span></span>

<span data-ttu-id="85a7d-535">모든 프로덕션 트래픽에 대해 이 기능을 기본 비활성 상태로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-535">For all production traffic, it is highly recommended to leave this feature in its default disabled state.</span></span> <span data-ttu-id="85a7d-536">그렇지 않으면 실수로 웹 페이지를 새로 고칠 때 많은 no-cache 요청을 트리거할 수 있는 최종 사용자 또는 모든 비디오 요청과 함께 no-cache 헤더를 보내도록 코딩된 인기 있는 다양한 미디어 플레이어로부터 원본 서버를 보호하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-536">Otherwise, origin servers will not be shielded from end-users who may inadvertently trigger many no-cache requests when refreshing web pages, or from the many popular media players that are coded to send a no-cache header with every video request.</span></span> <span data-ttu-id="85a7d-537">그럼에도 불구하고 이 기능은 원본 서버에서 요청 시 새로운 콘텐츠를 끌어올 수 있도록 특정 비프로덕션 스테이징 또는 테스트 디렉터리에 적용하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-537">Nevertheless, this feature can be useful to apply to certain non-production staging or testing directories, in order to allow fresh content to be pulled on-demand from the origin server.</span></span>

<span data-ttu-id="85a7d-538">이 기능에 따라 원본 서버로 전달하도록 허용되는 요청에 대해 보고할 캐시 상태는 TCP_Client_Refresh_Miss입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-538">The cache status that will be reported for a request that is allowed to be forwarded to an origin server due to this feature is TCP_Client_Refresh_Miss.</span></span> <span data-ttu-id="85a7d-539">코어 보고 모듈에서 사용할 수 있는 캐시 상태 보고서는 캐시 상태별 통계 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-539">The Cache Statuses report, which is available in the Core reporting module, provides statistical information by cache status.</span></span> <span data-ttu-id="85a7d-540">이렇게 하면 이 기능에 따라 원본 서버로 전달하는 요청의 수와 백분율을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-540">This allows you to track the number and percentage of requests that are being forwarded to an origin server due to this feature.</span></span>

<span data-ttu-id="85a7d-541">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-541">**Default Behavior:** Disabled.</span></span>

###<a name="ignore-origin-no-cache"></a><span data-ttu-id="85a7d-542">원본 no-cache 무시</span><span class="sxs-lookup"><span data-stu-id="85a7d-542">Ignore Origin no-cache</span></span>
<span data-ttu-id="85a7d-543">**목적:** CDN에서 원본 서버로부터 제공되는 다음 지시문을 무시할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-543">**Purpose:** Determines whether our CDN will ignore the following directives served from an origin server:</span></span>

- <span data-ttu-id="85a7d-544">Cache-Control: private</span><span class="sxs-lookup"><span data-stu-id="85a7d-544">Cache-Control: private</span></span>
- <span data-ttu-id="85a7d-545">Cache-Control: no-store</span><span class="sxs-lookup"><span data-stu-id="85a7d-545">Cache-Control: no-store</span></span>
- <span data-ttu-id="85a7d-546">Cache-Control: no-cache</span><span class="sxs-lookup"><span data-stu-id="85a7d-546">Cache-Control: no-cache</span></span>
- <span data-ttu-id="85a7d-547">Pragma: no-cache</span><span class="sxs-lookup"><span data-stu-id="85a7d-547">Pragma: no-cache</span></span>

<span data-ttu-id="85a7d-548">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-548">Key information:</span></span>

- <span data-ttu-id="85a7d-549">위의 지시문을 무시할 상태 코드의 공백으로 구분된 목록을 정의하여 이 기능을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-549">Configure this feature by defining a space-delimited list of status codes for which the above directives will be ignored.</span></span>
- <span data-ttu-id="85a7d-550">이 기능에 대한 유효한 상태 코드 집합은 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 및 505입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-550">The set of valid status codes for this feature are: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, and 505.</span></span>
- <span data-ttu-id="85a7d-551">이 기능을 빈 값으로 설정하면 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-551">Disable this feature by setting it to a blank value.</span></span>
- <span data-ttu-id="85a7d-552">캐시 설정을 추적하는 방식으로 인해 이 기능은 다음 일치 조건과 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-552">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following match conditions:</span></span> 
    - <span data-ttu-id="85a7d-553">에지</span><span class="sxs-lookup"><span data-stu-id="85a7d-553">Edge</span></span> 
    - <span data-ttu-id="85a7d-554">Cname</span><span class="sxs-lookup"><span data-stu-id="85a7d-554">Cname</span></span>
    - <span data-ttu-id="85a7d-555">요청 헤더 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-555">Request Header Literal</span></span>
    - <span data-ttu-id="85a7d-556">요청 헤더 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-556">Request Header Wildcard</span></span>
    - <span data-ttu-id="85a7d-557">요청 메서드</span><span class="sxs-lookup"><span data-stu-id="85a7d-557">Request Method</span></span>
    - <span data-ttu-id="85a7d-558">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-558">URL Query Literal</span></span>
    - <span data-ttu-id="85a7d-559">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-559">URL Query Wildcard</span></span>

<span data-ttu-id="85a7d-560">**기본 동작:** 위의 지시문을 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-560">**Default Behavior:** The default behavior is to honor the above directives.</span></span>

###<a name="ignore-unsatisfiable-ranges"></a><span data-ttu-id="85a7d-561">적절하지 않은 범위 무시</span><span class="sxs-lookup"><span data-stu-id="85a7d-561">Ignore Unsatisfiable Ranges</span></span> 
<span data-ttu-id="85a7d-562">**목적:** 요청에서 416 요청한 범위가 충분하지 않음 상태 코드를 생성하는 경우 클라이언트로 반환할 응답을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-562">**Purpose:** Determines the response that will be returned to clients when a request generates a 416 Requested Range Not Satisfiable status code.</span></span>

<span data-ttu-id="85a7d-563">기본적으로 에지 서버에서 지정된 바이트 범위 요청을 충족할 수 없고 If-Range 요청 헤더 필드를 지정하지 않은 경우에 이 상태 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-563">By default, this status code is returned when the specified byte-range request cannot be satisfied by an edge server and an If-Range request header field was not specified.</span></span>

<span data-ttu-id="85a7d-564">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-564">Value</span></span>|<span data-ttu-id="85a7d-565">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-565">Result</span></span>
-|-
<span data-ttu-id="85a7d-566">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-566">Enabled</span></span>|<span data-ttu-id="85a7d-567">에지 서버에서 416 요청한 범위가 충분하지 않음 상태 코드의 잘못된 바이트 범위 요청에 응답하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-567">Prevents our edge servers from responding to an invalid byte-range request with a 416 Requested Range Not Satisfiable status code.</span></span> <span data-ttu-id="85a7d-568">대신 서버에서 요청된 자산을 제공하고 클라이언트에 200 확인을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-568">Instead our servers will deliver the requested asset and return a 200 OK to the client.</span></span>
<span data-ttu-id="85a7d-569">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-569">Disabled</span></span>|<span data-ttu-id="85a7d-570">기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-570">Restores the default behavior.</span></span> <span data-ttu-id="85a7d-571">기본 동작은 416 요청한 범위가 충분하지 않음 상태 코드를 허용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-571">The default behavior is to honor the 416 Requested Range Not Satisfiable status code.</span></span>

<span data-ttu-id="85a7d-572">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-572">**Default Behavior:** Disabled.</span></span>

###<a name="internal-max-stale"></a><span data-ttu-id="85a7d-573">내부 Max-Stale</span><span class="sxs-lookup"><span data-stu-id="85a7d-573">Internal Max-Stale</span></span>
<span data-ttu-id="85a7d-574">**목적:** 에지 서버에서 원본 서버와 함께 캐시된 자산의 유효성 재검사를 수행할 수 없는 경우 에지 서버에서 캐시된 자산을 제공할 수 있는 정상 만료 시간을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-574">**Purpose:** Controls how long past the normal expiration time a cached asset may be served from an edge server when the edge server is unable to revalidate the cached asset with the origin server.</span></span>

<span data-ttu-id="85a7d-575">일반적으로 자산의 max-age 간격이 만료되면 에지 서버에서 유효성 재검사 요청을 원본 서버로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-575">Normally, when an asset's max-age time expires, the edge server will send a revalidation request to the origin server.</span></span> <span data-ttu-id="85a7d-576">그런 다음 원본 서버에서 304 수정되지 않음으로 응답하여 캐시된 자산을 에지 서버에 새로 빌려주거나, 그렇지 않으면 200 확인을 사용하여 캐시된 자산의 업데이트된 버전을 에지 서버에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-576">The origin server will then respond with either a 304 Not Modified to give the edge server a fresh lease on the cached asset, or else with 200 OK to provide the edge server with an updated version of the cached asset.</span></span>

<span data-ttu-id="85a7d-577">이러한 유효성 재검사를 시도하는 동안 에지 서버에서 원본 서버와의 연결을 설정할 수 없는 경우 내부 Max-Stale 기능은 에지 서버에서 현재의 부실 자산을 계속 제공할지 여부와 기간을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-577">If the edge server is unable to establish a connection with the origin server while attempting such a revalidation, then this Internal Max-Stale feature controls whether, and for how long, the edge server may continue to serve the now-stale asset.</span></span>

<span data-ttu-id="85a7d-578">이 시간 간격은 실패한 유효성 재검사를 수행할 때가 아니라 자산의 max-age 간격이 만료될 때 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-578">Note that this time interval starts when the asset's max-age expires, not when the failed revalidation occurs.</span></span> <span data-ttu-id="85a7d-579">따라서 성공적인 유효성 재검사 없이 자산을 제공할 수 있는 최대 기간은 max-age와 max-stale의 조합으로 지정된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-579">Therefore, the maximum period during which an asset can be served without successful revalidation is the amount of time specified by the combination of max-age plus max-stale.</span></span> <span data-ttu-id="85a7d-580">예를 들어 자산을 9시 00분에 30분의 max-age 및 15분의 max-stale 간격으로 캐시한 경우 9시 44분에 실패한 유효성 재검사 시도는 최종 사용자에게 캐시된 부실 자산을 제공하는 반면 9시 46분에 실패한 유효성 재검사 시도는 최종 사용자에게 504 게이트웨이 시간 초과를 제공하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-580">For example, if an asset was cached at 9:00 with a max-age of 30 minutes and a max-stale of 15 minutes, then a failed revalidation attempt at 9:44 would result in an end-user receiving the stale cached asset, while a failed revalidation attempt at 9:46 would result in the end user receiving a 504 Gateway Timeout.</span></span>

<span data-ttu-id="85a7d-581">이 기능에 구성된 값은 원본 서버로부터 수신한 Cache-Control:must-revalidate 또는 Cache-Control:proxy-revalidate 헤더로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-581">Any value configured for this feature is superseded by Cache-Control:must-revalidate or Cache-Control:proxy-revalidate headers received from the origin server.</span></span> <span data-ttu-id="85a7d-582">자산을 처음 캐시할 때 원본 서버로부터 이러한 헤더 중 하나를 수신하면 에지 서버에서 캐시된 부실 자산을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-582">If either of those headers is received from the origin server when an asset is initially cached, then the edge server will not serve a stale cached asset.</span></span> <span data-ttu-id="85a7d-583">이러한 경우 자산의 max-age 간격이 만료되었을 때 에지 서버에서 원본 서버와 함께 유효성을 재검사할 수 없는 경우 에지 서버에서 504 게이트웨이 시간 초과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-583">In such a case, if the edge server is unable to revalidate with the origin when the asset's max-age interval has expired, then the edge server will return a 504 Gateway Timeout.</span></span>

<span data-ttu-id="85a7d-584">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-584">Key information:</span></span>

- <span data-ttu-id="85a7d-585">이 기능은 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-585">Configure this feature by:</span></span>
    - <span data-ttu-id="85a7d-586">max-stale 간격을 적용할 상태 코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-586">Selecting the status code for which a max-stale will be applied.</span></span>
    - <span data-ttu-id="85a7d-587">정수 값을 지정한 다음 원하는 시간 단위(즉 초, 분, 시간 등)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-587">Specifying an integer value and then selecting the desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="85a7d-588">이 값은 적용할 내부 max-stale 간격을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-588">This value defines the internal max-stale that will be applied.</span></span>

- <span data-ttu-id="85a7d-589">시간 단위를 "끄기"로 설정하면 이 기능을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-589">Setting the time unit to "Off" will disable this feature.</span></span> <span data-ttu-id="85a7d-590">캐시된 자산은 정상 만료 시간을 초과하여 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-590">A cached asset will not be served beyond its normal expiration time.</span></span>
- <span data-ttu-id="85a7d-591">캐시 설정을 추적하는 방식으로 인해 이 기능은 다음 일치 조건과 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-591">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following match conditions:</span></span> 
    - <span data-ttu-id="85a7d-592">에지</span><span class="sxs-lookup"><span data-stu-id="85a7d-592">Edge</span></span> 
    - <span data-ttu-id="85a7d-593">Cname</span><span class="sxs-lookup"><span data-stu-id="85a7d-593">Cname</span></span>
    - <span data-ttu-id="85a7d-594">요청 헤더 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-594">Request Header Literal</span></span>
    - <span data-ttu-id="85a7d-595">요청 헤더 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-595">Request Header Wildcard</span></span>
    - <span data-ttu-id="85a7d-596">요청 메서드</span><span class="sxs-lookup"><span data-stu-id="85a7d-596">Request Method</span></span>
    - <span data-ttu-id="85a7d-597">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-597">URL Query Literal</span></span>
    - <span data-ttu-id="85a7d-598">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-598">URL Query Wildcard</span></span>

<span data-ttu-id="85a7d-599">**기본 동작:** 2분</span><span class="sxs-lookup"><span data-stu-id="85a7d-599">**Default Behavior:** 2 minutes</span></span>

###<a name="partial-cache-sharing"></a><span data-ttu-id="85a7d-600">부분 캐시 공유</span><span class="sxs-lookup"><span data-stu-id="85a7d-600">Partial Cache Sharing</span></span>
<span data-ttu-id="85a7d-601">**목적:** 요청에서 부분적으로 캐시된 콘텐츠를 생성할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-601">**Purpose:** Determines whether a request can generate partially cached content.</span></span>

<span data-ttu-id="85a7d-602">이 부분 캐시는 요청된 콘텐츠를 완전히 캐시할 때까지 해당 콘텐츠에 대한 새 요청을 수행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-602">This partial cache may then be used to fulfill new requests for that content until the requested content is fully cached.</span></span>

<span data-ttu-id="85a7d-603">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-603">Value</span></span>|<span data-ttu-id="85a7d-604">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-604">Result</span></span>
-|-
<span data-ttu-id="85a7d-605">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-605">Enabled</span></span>|<span data-ttu-id="85a7d-606">요청에서 부분적으로 캐시된 콘텐츠를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-606">Requests can generate partially cached content.</span></span>
<span data-ttu-id="85a7d-607">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-607">Disabled</span></span>|<span data-ttu-id="85a7d-608">요청에서 요청한 콘텐츠에 대해 완전하게 캐시된 버전만 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-608">Requests can only generate a fully cached version of the requested content.</span></span>

<span data-ttu-id="85a7d-609">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-609">**Default Behavior:** Disabled.</span></span>

###<a name="prevalidate-cached-content"></a><span data-ttu-id="85a7d-610">캐시된 콘텐츠 사전 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="85a7d-610">Prevalidate Cached Content</span></span>
<span data-ttu-id="85a7d-611">**목적:** TTL이 만료되기 전에 캐시된 콘텐츠가 초기 유효성 재검사에 적합한지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-611">**Purpose:** Determines whether cached content will be eligible for early revalidation before its TTL expires.</span></span>

<span data-ttu-id="85a7d-612">초기 유효성 재검사에 적합한 동안 요청된 콘텐츠의 TTL이 만료되기까지의 시간을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-612">Define the amount of time prior to the expiration of the requested content's TTL during which it will be eligible for early revalidation.</span></span>

<span data-ttu-id="85a7d-613">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-613">Key information:</span></span>

- <span data-ttu-id="85a7d-614">시간 단위를 "끄기"로 선택하여 캐시된 콘텐츠의 TTL이 만료된 후에 유효성 재검사를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-614">Selecting "Off" as the time unit requires revalidation to take place after the cached content's TTL has expired.</span></span> <span data-ttu-id="85a7d-615">시간은 지정하지 않아야 하며, 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-615">Time should not be specified and it will be ignored.</span></span>

<span data-ttu-id="85a7d-616">**기본 동작:** 끄기</span><span class="sxs-lookup"><span data-stu-id="85a7d-616">**Default Behavior:** Off.</span></span> <span data-ttu-id="85a7d-617">유효성 재검사는 캐시된 콘텐츠의 TTL이 만료된 후에만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-617">Revalidation may only take place after the cached content's TTL has expired.</span></span>

###<a name="refresh-zero-byte-cache-files"></a><span data-ttu-id="85a7d-618">0바이트 캐시 파일 새로 고침</span><span class="sxs-lookup"><span data-stu-id="85a7d-618">Refresh Zero Byte Cache Files</span></span>
<span data-ttu-id="85a7d-619">**목적:** 에지 서버에서 0바이트 캐시 자산에 대한 HTTP 클라이언트 요청을 처리하는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-619">**Purpose:** Determines how an HTTP client's request for a 0-byte cache asset is handled by our edge servers.</span></span>

<span data-ttu-id="85a7d-620">유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-620">Valid values are:</span></span>

<span data-ttu-id="85a7d-621">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-621">Value</span></span>|<span data-ttu-id="85a7d-622">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-622">Result</span></span>
--|--
<span data-ttu-id="85a7d-623">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-623">Enabled</span></span>|<span data-ttu-id="85a7d-624">에지 서버에서 원본 서버로부터 자산을 다시 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-624">Causes our edge server to re-fetch the asset from the origin server.</span></span>
<span data-ttu-id="85a7d-625">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-625">Disabled</span></span>|<span data-ttu-id="85a7d-626">기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-626">Restores the default behavior.</span></span> <span data-ttu-id="85a7d-627">기본 동작은 요청 시 유효한 캐시 자산을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-627">The default behavior is to serve up valid cache assets upon request.</span></span>
<span data-ttu-id="85a7d-628">이 기능은 올바른 캐싱 및 콘텐츠 배달에는 필요하지 않지만 해결 방법으로는 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-628">This feature is not required for correct caching and content delivery, but may be useful as a workaround.</span></span> <span data-ttu-id="85a7d-629">예를 들어 원본 서버의 동적 콘텐츠 생성기로 인해 실수로 0바이트 응답을 에지 서버로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-629">For example, dynamic content generators on origin servers can inadvertently result in 0-byte responses being sent to the edge servers.</span></span> <span data-ttu-id="85a7d-630">이러한 유형의 응답은 일반적으로 에지 서버에서 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-630">These types of responses are typically cached by our edge servers.</span></span> <span data-ttu-id="85a7d-631">0바이트 응답이 이러한 콘텐츠에 대해 유효한 응답이 아님을 알고 있는 경우</span><span class="sxs-lookup"><span data-stu-id="85a7d-631">If you know that a 0-byte response is never a valid response</span></span> 

<span data-ttu-id="85a7d-632">이 기능을 통해 이러한 유형의 자산을 클라이언트에 제공하지 못하도록 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-632">for such content, then this feature can prevent these types of assets from being served to your clients.</span></span>

<span data-ttu-id="85a7d-633">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-633">**Default Behavior:** Disabled.</span></span>

###<a name="set-cacheable-status-codes"></a><span data-ttu-id="85a7d-634">캐시 가능한 상태 코드 집합</span><span class="sxs-lookup"><span data-stu-id="85a7d-634">Set Cacheable Status Codes</span></span>
<span data-ttu-id="85a7d-635">**목적:** 캐시된 콘텐츠를 가져올 수 있는 상태 코드 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-635">**Purpose:** Defines the set of status codes that can result in cached content.</span></span>

<span data-ttu-id="85a7d-636">기본적으로 캐싱은 200 확인 응답에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-636">By default, caching is only enabled for 200 OK responses.</span></span>

<span data-ttu-id="85a7d-637">원하는 상태 코드의 공백으로 구분된 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-637">Define a space-delimited set of the desired status codes.</span></span>

<span data-ttu-id="85a7d-638">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-638">Key information:</span></span>

- <span data-ttu-id="85a7d-639">원본 No-Cache 무시 기능도 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-639">Please also enable the Ignore Origin No-Cache feature.</span></span> <span data-ttu-id="85a7d-640">해당 기능을 사용할 수 없으면 비 200 확인 응답이 캐시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-640">If that feature is not enabled, then non-200 OK responses may not be cached.</span></span>
- <span data-ttu-id="85a7d-641">이 기능에 대한 유효한 상태 코드 집합은 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 및 505입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-641">The set of valid status codes for this feature are: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, and 505.</span></span>
- <span data-ttu-id="85a7d-642">이 기능은 200 확인 상태 코드를 생성하는 응답의 캐싱을 비활성화하는 데 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-642">This feature cannot be used to disable caching for responses that generate a 200 OK status code.</span></span>

<span data-ttu-id="85a7d-643">**기본 동작:** 캐싱은 200 확인 상태 코드를 생성하는 응답에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-643">**Default Behavior:** Caching is only enabled for responses that generate a 200 OK status code.</span></span>
###<a name="stale-content-delivery-on-error"></a><span data-ttu-id="85a7d-644">오류 시 오래된 콘텐츠 배달</span><span class="sxs-lookup"><span data-stu-id="85a7d-644">Stale Content Delivery on Error</span></span>
<span data-ttu-id="85a7d-645">**목적:**</span><span class="sxs-lookup"><span data-stu-id="85a7d-645">**Purpose:**</span></span> 

<span data-ttu-id="85a7d-646">캐시 유효성 재검사 중이나 고객 원본 서버에서 요청된 콘텐츠를 검색할 때 만료되고 캐시된 콘텐츠를 배달할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-646">Determines whether expired cached content will be delivered when an error occurs during cache revalidation or when retrieving the requested content from the customer origin server.</span></span>

<span data-ttu-id="85a7d-647">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-647">Value</span></span>|<span data-ttu-id="85a7d-648">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-648">Result</span></span>
-|-
<span data-ttu-id="85a7d-649">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-649">Enabled</span></span>|<span data-ttu-id="85a7d-650">원본 서버에 연결하는 동안 오류가 발생하면 요청자에게 부실 콘텐츠를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-650">Stale content will be served to the requester when an error occurs during a connection to an origin server.</span></span>
<span data-ttu-id="85a7d-651">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-651">Disabled</span></span>|<span data-ttu-id="85a7d-652">요청자에게 원본 서버의 오류를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-652">The origin server's error will be forwarded to the requester.</span></span>

<span data-ttu-id="85a7d-653">**기본 동작:** 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-653">**Default Behavior:** Disabled</span></span>

###<a name="stale-while-revalidate"></a><span data-ttu-id="85a7d-654">유효성 재검사 중 기한 경과</span><span class="sxs-lookup"><span data-stu-id="85a7d-654">Stale While Revalidate</span></span>
<span data-ttu-id="85a7d-655">**목적:** 유효성 재검사를 수행하는 동안 에지 서버에서 요청자에게 부실 콘텐츠를 제공하도록 하여 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-655">**Purpose:** Improves performance by allowing our edge servers to serve stale content to the requester while revalidation takes place.</span></span>

<span data-ttu-id="85a7d-656">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-656">Key information:</span></span>

- <span data-ttu-id="85a7d-657">이 기능의 동작은 선택한 시간 단위에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-657">The behavior of this feature varies according to the selected time unit.</span></span>
    - <span data-ttu-id="85a7d-658">**시간 단위:** 부실 콘텐츠 배달을 허용하려면 기간을 지정하고 시간 단위(예: 초, 분, 시간 등)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-658">**Time Unit:** Specify a length of time and select a time unit (e.g., Seconds, Minutes, Hours, etc.) to allow stale content delivery.</span></span> <span data-ttu-id="85a7d-659">이 유형의 설정을 사용하면 CDN에서 **TTL** + **유효성 재검사 중 기한 경과 시간** 수식에 따라 유효성 검사를 요구하기 전에 콘텐츠를 배달할 수 있는 기간을 연장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-659">This type of setup allows the CDN to extend the length of time that it may deliver content before requiring validation according to the following formula:**TTL** + **Stale While Revalidate Time**</span></span> 
    - <span data-ttu-id="85a7d-660">**끄기:** 부실 콘텐츠에 대한 요청을 처리할 수 있기 전에 유효성 재검사를 요구하려면 "끄기"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-660">**Off:** Select "Off" to require revalidation before a request for stale content may be served.</span></span>
        - <span data-ttu-id="85a7d-661">기간은 적용할 수 없으므로 지정하지 않아야 하며, 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-661">Do not specify a length of time since it is inapplicable and will be ignored.</span></span>

<span data-ttu-id="85a7d-662">**기본 동작:** 끄기</span><span class="sxs-lookup"><span data-stu-id="85a7d-662">**Default Behavior:** Off.</span></span> <span data-ttu-id="85a7d-663">유효성 재검사는 요청된 콘텐츠를 제공할 수 있기 전에 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-663">Revalidation must take place before the requested content can be served.</span></span>

###<a name="comment"></a><span data-ttu-id="85a7d-664">주석</span><span class="sxs-lookup"><span data-stu-id="85a7d-664">Comment</span></span>
<span data-ttu-id="85a7d-665">**목적:** 규칙 내에 주석을 추가할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-665">**Purpose:** Allows a note to be added within a rule.</span></span>

<span data-ttu-id="85a7d-666">이 기능의 한 가지 용도는 규칙의 일반 목적 또는 특정 일치 조건이나 기능을 규칙에 추가한 이유에 대한 추가 정보를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-666">One use for this feature is to provide additional information on the general purpose of a rule or why a particular match condition or feature was added to the rule.</span></span>

<span data-ttu-id="85a7d-667">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-667">Key information:</span></span>

- <span data-ttu-id="85a7d-668">최대 150자를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-668">A maximum of 150 characters may be specified.</span></span>
- <span data-ttu-id="85a7d-669">영숫자만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-669">Make sure to only use alphanumeric characters.</span></span>
- <span data-ttu-id="85a7d-670">이 기능은 규칙의 동작에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-670">This feature does not affect the behavior of the rule.</span></span> <span data-ttu-id="85a7d-671">단지 나중에 참조할 수 있도록 정보를 제공하거나 규칙 문제를 해결할 때 도움이 될 수 있는 영역을 제공하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-671">It is merely meant to provide an area where you can provide information for future reference or that may help when troubleshooting the rule.</span></span>
 
## <a name="headers"></a><span data-ttu-id="85a7d-672">헤더</span><span class="sxs-lookup"><span data-stu-id="85a7d-672">Headers</span></span>

<span data-ttu-id="85a7d-673">이러한 기능은 요청자 또는 응답에서 헤더를 추가, 수정 또는 삭제하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-673">These features are designed to add, modify, or delete headers from the request or response.</span></span>

<span data-ttu-id="85a7d-674">이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-674">Name</span></span> | <span data-ttu-id="85a7d-675">목적</span><span class="sxs-lookup"><span data-stu-id="85a7d-675">Purpose</span></span>
-----|--------
<span data-ttu-id="85a7d-676">Age 응답 헤더</span><span class="sxs-lookup"><span data-stu-id="85a7d-676">Age Response Header</span></span> | <span data-ttu-id="85a7d-677">Age 응답 헤더를 요청자에게 전송되는 응답에 포함할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-677">Determines whether an Age response header will be included in the response sent to the requester.</span></span>
<span data-ttu-id="85a7d-678">디버그 캐시 응답 헤더</span><span class="sxs-lookup"><span data-stu-id="85a7d-678">Debug Cache Response Headers</span></span> | <span data-ttu-id="85a7d-679">응답에 요청된 자산에 대한 캐시 정책 정보를 제공하는 X-EC-Debug 응답 헤더를 포함할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-679">Determines whether a response may include the X-EC-Debug response header which provides information on the cache policy for the requested asset.</span></span>
<span data-ttu-id="85a7d-680">클라이언트 요청 헤더 수정</span><span class="sxs-lookup"><span data-stu-id="85a7d-680">Modify Client Request Header</span></span> | <span data-ttu-id="85a7d-681">요청에서 헤더를 덮어쓰기, 추가 또는 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-681">Overwrites, appends, or deletes a header from a request.</span></span>
<span data-ttu-id="85a7d-682">클라이언트 응답 헤더 수정</span><span class="sxs-lookup"><span data-stu-id="85a7d-682">Modify Client Response Header</span></span> | <span data-ttu-id="85a7d-683">응답에서 헤더를 덮어쓰기, 추가 또는 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-683">Overwrites, appends, or deletes a header from a response.</span></span>
<span data-ttu-id="85a7d-684">클라이언트 IP 사용자 지정 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="85a7d-684">Set Client IP Custom Header</span></span> | <span data-ttu-id="85a7d-685">클라이언트를 요청하는 IP 주소가 사용자 지정 요청 헤더로 요청에 추가되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-685">Allows the IP address of the requesting client to be added to the request as a custom request header.</span></span>

###<a name="age-response-header"></a><span data-ttu-id="85a7d-686">Age 응답 헤더</span><span class="sxs-lookup"><span data-stu-id="85a7d-686">Age Response Header</span></span>
<span data-ttu-id="85a7d-687">**목적:** 요청자에게 보내는 응답에 Age 응답 헤더를 포함할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-687">**Purpose**: Determines whether an Age response header will be included in the response sent to the requester.</span></span>
<span data-ttu-id="85a7d-688">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-688">Value</span></span>|<span data-ttu-id="85a7d-689">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-689">Result</span></span>
--|--
<span data-ttu-id="85a7d-690">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-690">Enabled</span></span> | <span data-ttu-id="85a7d-691">요청자에게 보내는 응답에 Age 응답 헤더를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-691">The Age response header will be included in the response sent to the requester.</span></span>
<span data-ttu-id="85a7d-692">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-692">Disabled</span></span> | <span data-ttu-id="85a7d-693">요청자에게 보내는 응답에서 Age 응답 헤더를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-693">The Age response header will be excluded from the response sent to the requester.</span></span>

<span data-ttu-id="85a7d-694">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-694">**Default Behavior**: Disabled.</span></span>

###<a name="debug-cache-response-headers"></a><span data-ttu-id="85a7d-695">디버그 캐시 응답 헤더</span><span class="sxs-lookup"><span data-stu-id="85a7d-695">Debug Cache Response Headers</span></span>
<span data-ttu-id="85a7d-696">**목적:** 요청된 자산에 대한 캐시 정책 정보를 제공하는 X-EC-Debug 응답 헤더를 응답에 포함할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-696">**Purpose:** Determines whether a response may include the X-EC-Debug response header which provides information on the cache policy for the requested asset.</span></span>

<span data-ttu-id="85a7d-697">디버그 캐시 응답 헤더는 다음 두 가지 모두에 해당하는 경우 응답에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-697">Debug cache response headers will be included in the response when both of the following are true:</span></span>

- <span data-ttu-id="85a7d-698">디버그 캐시 응답 헤더 기능은 원하는 요청에서 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-698">The Debug Cache Response Headers Feature has been enabled on the desired request.</span></span>
- <span data-ttu-id="85a7d-699">위의 요청은 응답에 포함될 디버그 캐시 응답 헤더 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-699">The above request defines the set of debug cache response headers that will be included in the response.</span></span>

<span data-ttu-id="85a7d-700">디버그 캐시 응답 헤더는 다음 헤더 및 원하는 지시문을 요청에 포함하여 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-700">Debug cache response headers may be requested by including the following header and the desired directives in the request:</span></span>

<span data-ttu-id="85a7d-701">X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_</span><span class="sxs-lookup"><span data-stu-id="85a7d-701">X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_</span></span>

<span data-ttu-id="85a7d-702">**예제:**</span><span class="sxs-lookup"><span data-stu-id="85a7d-702">**Example:**</span></span>

<span data-ttu-id="85a7d-703">X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state</span><span class="sxs-lookup"><span data-stu-id="85a7d-703">X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state</span></span>

<span data-ttu-id="85a7d-704">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-704">Value</span></span>|<span data-ttu-id="85a7d-705">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-705">Result</span></span>
-|-
<span data-ttu-id="85a7d-706">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-706">Enabled</span></span>|<span data-ttu-id="85a7d-707">디버그 캐시 응답 헤더에 대한 요청에서 X-EC-Debug 헤더를 포함한 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-707">Requests for debug cache response headers will return a response that includes the X-EC-Debug header.</span></span>
<span data-ttu-id="85a7d-708">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-708">Disabled</span></span>|<span data-ttu-id="85a7d-709">X-EC-Debug 응답 헤더가 응답에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-709">The X-EC-Debug response header will be excluded from the response.</span></span>

<span data-ttu-id="85a7d-710">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-710">**Default Behavior:** Disabled.</span></span>

###<a name="modify-client-response-header"></a><span data-ttu-id="85a7d-711">클라이언트 응답 헤더 수정</span><span class="sxs-lookup"><span data-stu-id="85a7d-711">Modify Client Response Header</span></span>
<span data-ttu-id="85a7d-712">**목적:** 각 요청에는 이를 설명하는 [요청 헤더]() 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-712">**Purpose:** Each request contains a set of [request headers]() that describe it.</span></span> <span data-ttu-id="85a7d-713">이 기능은 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-713">This feature can either:</span></span>

- <span data-ttu-id="85a7d-714">요청 헤더에 할당된 값을 추가하거나 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-714">Append or overwrite the value assigned to a request header.</span></span> <span data-ttu-id="85a7d-715">지정된 요청 헤더가 없는 경우 이 기능은 요청에 해당 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-715">If the specified request header does not exist, then this feature will add it to the request.</span></span>
- <span data-ttu-id="85a7d-716">요청에서 요청 헤더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-716">Delete a request header from the request.</span></span>

<span data-ttu-id="85a7d-717">원본 서버로 전달되는 요청에는 이 기능에서 변경한 내용이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-717">Requests that are forwarded to an origin server will reflect the changes made by this feature.</span></span>

<span data-ttu-id="85a7d-718">요청 헤더에서 다음 작업 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-718">One of the following actions can be performed on a request header:</span></span>

<span data-ttu-id="85a7d-719">옵션</span><span class="sxs-lookup"><span data-stu-id="85a7d-719">Option</span></span>|<span data-ttu-id="85a7d-720">설명</span><span class="sxs-lookup"><span data-stu-id="85a7d-720">Description</span></span>|<span data-ttu-id="85a7d-721">예</span><span class="sxs-lookup"><span data-stu-id="85a7d-721">Example</span></span>
-|-|-
<span data-ttu-id="85a7d-722">추가</span><span class="sxs-lookup"><span data-stu-id="85a7d-722">Append</span></span>|<span data-ttu-id="85a7d-723">지정된 값을 기존 요청 헤더 값의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-723">The specified value will be added toend of the existing request header value.</span></span>|<span data-ttu-id="85a7d-724">**요청 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="85a7d-724">**Request header value (Client):**Value1</span></span> <br/> <span data-ttu-id="85a7d-725">**요청 헤더 값(HTTP 규칙 엔진):** Value2</span><span class="sxs-lookup"><span data-stu-id="85a7d-725">**Request header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="85a7d-726">**새 요청 헤더 값:** Value1Value2</span><span class="sxs-lookup"><span data-stu-id="85a7d-726">**New request header value:** Value1Value2</span></span>
<span data-ttu-id="85a7d-727">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-727">Overwrite</span></span>|<span data-ttu-id="85a7d-728">요청 헤더 값을 지정된 된 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-728">The request header value will be set to the specified value.</span></span>|<span data-ttu-id="85a7d-729">**요청 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="85a7d-729">**Request header value (Client):**Value1</span></span> <br/><span data-ttu-id="85a7d-730">**요청 헤더 값(HTTP 규칙 엔진):** Value2</span><span class="sxs-lookup"><span data-stu-id="85a7d-730">**Request header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="85a7d-731">**새 요청 헤더 값:** Value2</span><span class="sxs-lookup"><span data-stu-id="85a7d-731">**New request header value:** Value2</span></span> <br/>
<span data-ttu-id="85a7d-732">삭제</span><span class="sxs-lookup"><span data-stu-id="85a7d-732">Delete</span></span>|<span data-ttu-id="85a7d-733">지정된 요청 헤더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-733">Deletes the specified request header.</span></span>|<span data-ttu-id="85a7d-734">**요청 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="85a7d-734">**Request header value (Client):**Value1</span></span> <br/> <span data-ttu-id="85a7d-735">**클라이언트 요청 헤더 수정 구성:** 문제의 요청 헤더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-735">**Modify Client Request Header configuration:** Delete the request header in question.</span></span> <br/><span data-ttu-id="85a7d-736">**결과:** 지정된 요청 헤더를 원본 서버로 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-736">**Result:** The specified request header will not be forwarded to the origin server.</span></span>

<span data-ttu-id="85a7d-737">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-737">Key information:</span></span>

- <span data-ttu-id="85a7d-738">이름 옵션에 지정된 값이 원하는 요청 헤더와 정확히 일치해야 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-738">Make sure that the value specified in the Name option is an exact match for the desired request header.</span></span>
- <span data-ttu-id="85a7d-739">헤더를 식별하기 위해 사례를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-739">Case is not taken into account for the purpose of identifying a header.</span></span> <span data-ttu-id="85a7d-740">예를 들어 다음과 같은 Cache-Control 헤더 이름의 변형을 사용하여 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-740">For example, any of the following variations of the Cache-Control header name can be used to identify it:</span></span>
    - <span data-ttu-id="85a7d-741">cache-control</span><span class="sxs-lookup"><span data-stu-id="85a7d-741">cache-control</span></span>
    - <span data-ttu-id="85a7d-742">CACHE-CONTROL</span><span class="sxs-lookup"><span data-stu-id="85a7d-742">CACHE-CONTROL</span></span>
    - <span data-ttu-id="85a7d-743">cachE-Control</span><span class="sxs-lookup"><span data-stu-id="85a7d-743">cachE-Control</span></span>
- <span data-ttu-id="85a7d-744">헤더 이름을 지정할 때는 영숫자, 대시 또는 밑줄만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-744">Make sure to only use alphanumeric characters, dashes, or underscores when specifying a header name.</span></span>
- <span data-ttu-id="85a7d-745">헤더를 삭제하면 에지 서버에서 해당 헤더를 원본 서버로 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-745">Deleting a header will prevent it from being forwarded to an origin server by our edge servers.</span></span>
- <span data-ttu-id="85a7d-746">다음 헤더는 예약되어 있으며, 이 기능으로 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-746">The following headers are reserved and cannot be modified by this feature:</span></span>
    - <span data-ttu-id="85a7d-747">forwarded</span><span class="sxs-lookup"><span data-stu-id="85a7d-747">forwarded</span></span>
    - <span data-ttu-id="85a7d-748">host</span><span class="sxs-lookup"><span data-stu-id="85a7d-748">host</span></span>
    - <span data-ttu-id="85a7d-749">via</span><span class="sxs-lookup"><span data-stu-id="85a7d-749">via</span></span>
    - <span data-ttu-id="85a7d-750">Warning</span><span class="sxs-lookup"><span data-stu-id="85a7d-750">warning</span></span>
    - <span data-ttu-id="85a7d-751">x-forwarded-for</span><span class="sxs-lookup"><span data-stu-id="85a7d-751">x-forwarded-for</span></span>
    - <span data-ttu-id="85a7d-752">"x-ec"로 시작하는 모든 헤더 이름은 예약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-752">All header names that start with "x-ec" are reserved.</span></span>

###<a name="modify-client-response-header"></a><span data-ttu-id="85a7d-753">클라이언트 응답 헤더 수정</span><span class="sxs-lookup"><span data-stu-id="85a7d-753">Modify Client Response Header</span></span>
<span data-ttu-id="85a7d-754">각 응답에는 이를 설명하는 [응답 헤더]() 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-754">Each response contains a set of [response headers]() that describe it.</span></span> <span data-ttu-id="85a7d-755">이 기능은 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-755">This feature can either:</span></span>

- <span data-ttu-id="85a7d-756">응답 헤더에 할당된 값을 추가하거나 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-756">Append or overwrite the value assigned to a response header.</span></span> <span data-ttu-id="85a7d-757">지정된 요청 헤더가 없는 경우 이 기능은 응답에 해당 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-757">If the specified request header does not exist, then this feature will add it to the response.</span></span>
- <span data-ttu-id="85a7d-758">응답에서 응답 헤더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-758">Delete a response header from the response.</span></span>

<span data-ttu-id="85a7d-759">기본적으로 응답 헤더 값은 원본 서버 및 에지 서버에서 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-759">By default, response header values are defined by an origin server and by our edge servers.</span></span>

<span data-ttu-id="85a7d-760">응답 헤더에서 다음 작업 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-760">One of the following actions can be performed on a response header:</span></span>

<span data-ttu-id="85a7d-761">옵션</span><span class="sxs-lookup"><span data-stu-id="85a7d-761">Option</span></span>|<span data-ttu-id="85a7d-762">설명</span><span class="sxs-lookup"><span data-stu-id="85a7d-762">Description</span></span>|<span data-ttu-id="85a7d-763">예</span><span class="sxs-lookup"><span data-stu-id="85a7d-763">Example</span></span>
-|-|-
<span data-ttu-id="85a7d-764">추가</span><span class="sxs-lookup"><span data-stu-id="85a7d-764">Append</span></span>|<span data-ttu-id="85a7d-765">지정된 값을 기존 요청 헤더 값의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-765">The specified value will be added toend of the existing request header value.</span></span>|<span data-ttu-id="85a7d-766">**응답 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="85a7d-766">**Response header value (Client):**Value1</span></span> <br/> <span data-ttu-id="85a7d-767">**응답 헤더 값(HTTP 규칙 엔진):** Value2</span><span class="sxs-lookup"><span data-stu-id="85a7d-767">**Response header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="85a7d-768">**새 응답 헤더 값:** Value1Value2</span><span class="sxs-lookup"><span data-stu-id="85a7d-768">**New Response header value:** Value1Value2</span></span>
<span data-ttu-id="85a7d-769">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-769">Overwrite</span></span>|<span data-ttu-id="85a7d-770">요청 헤더 값을 지정된 된 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-770">The request header value will be set to the specified value.</span></span>|<span data-ttu-id="85a7d-771">**응답 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="85a7d-771">**Response header value (Client):**Value1</span></span> <br/><span data-ttu-id="85a7d-772">**응답 헤더 값(HTTP 규칙 엔진):** Value2</span><span class="sxs-lookup"><span data-stu-id="85a7d-772">**Response header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="85a7d-773">**새 응답 헤더 값:** Value2</span><span class="sxs-lookup"><span data-stu-id="85a7d-773">**New response header value:** Value2</span></span> <br/>
<span data-ttu-id="85a7d-774">삭제</span><span class="sxs-lookup"><span data-stu-id="85a7d-774">Delete</span></span>|<span data-ttu-id="85a7d-775">지정된 요청 헤더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-775">Deletes the specified request header.</span></span>|<span data-ttu-id="85a7d-776">**요청 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="85a7d-776">**Request header value (Client):** Value1</span></span> <br/> <span data-ttu-id="85a7d-777">**클라이언트 요청 헤더 수정 구성:** 문제의 응답 헤더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-777">**Modify Client Request Header configuration:** Delete the response header in question.</span></span> <br/><span data-ttu-id="85a7d-778">**결과:** 지정된 응답 헤더를 요청자에게 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-778">**Result:** The specified response header will not be forwarded to the requester.</span></span>

<span data-ttu-id="85a7d-779">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-779">Key information:</span></span>

- <span data-ttu-id="85a7d-780">이름 옵션에 지정된 값이 원하는 응답 헤더와 정확히 일치해야 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-780">Make sure that the value specified in the Name option is an exact match for the desired response header.</span></span> 
- <span data-ttu-id="85a7d-781">헤더를 식별하기 위해 사례를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-781">Case is not taken into account for the purpose of identifying a header.</span></span> <span data-ttu-id="85a7d-782">예를 들어 다음과 같은 Cache-Control 헤더 이름의 변형을 사용하여 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-782">For example, any of the following variations of the Cache-Control header name can be used to identify it:</span></span>
    - <span data-ttu-id="85a7d-783">cache-control</span><span class="sxs-lookup"><span data-stu-id="85a7d-783">cache-control</span></span>
    - <span data-ttu-id="85a7d-784">CACHE-CONTROL</span><span class="sxs-lookup"><span data-stu-id="85a7d-784">CACHE-CONTROL</span></span>
    - <span data-ttu-id="85a7d-785">cachE-Control</span><span class="sxs-lookup"><span data-stu-id="85a7d-785">cachE-Control</span></span>
- <span data-ttu-id="85a7d-786">헤더를 삭제하면 요청자에게 해당 헤더를 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-786">Deleting a header will prevent it from being forwarded to the requester.</span></span>
- <span data-ttu-id="85a7d-787">다음 헤더는 예약되어 있으며, 이 기능으로 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-787">The following headers are reserved and cannot be modified by this feature:</span></span>
    - <span data-ttu-id="85a7d-788">accept-encoding</span><span class="sxs-lookup"><span data-stu-id="85a7d-788">accept-encoding</span></span>
    - <span data-ttu-id="85a7d-789">age</span><span class="sxs-lookup"><span data-stu-id="85a7d-789">age</span></span>
    - <span data-ttu-id="85a7d-790">connection</span><span class="sxs-lookup"><span data-stu-id="85a7d-790">connection</span></span>
    - <span data-ttu-id="85a7d-791">content-encoding</span><span class="sxs-lookup"><span data-stu-id="85a7d-791">content-encoding</span></span>
    - <span data-ttu-id="85a7d-792">content-length</span><span class="sxs-lookup"><span data-stu-id="85a7d-792">content-length</span></span>
    - <span data-ttu-id="85a7d-793">content-range</span><span class="sxs-lookup"><span data-stu-id="85a7d-793">content-range</span></span>
    - <span data-ttu-id="85a7d-794">date</span><span class="sxs-lookup"><span data-stu-id="85a7d-794">date</span></span>
    - <span data-ttu-id="85a7d-795">server</span><span class="sxs-lookup"><span data-stu-id="85a7d-795">server</span></span>
    - <span data-ttu-id="85a7d-796">trailer</span><span class="sxs-lookup"><span data-stu-id="85a7d-796">trailer</span></span>
    - <span data-ttu-id="85a7d-797">transfer-encoding</span><span class="sxs-lookup"><span data-stu-id="85a7d-797">transfer-encoding</span></span>
    - <span data-ttu-id="85a7d-798">업그레이드</span><span class="sxs-lookup"><span data-stu-id="85a7d-798">upgrade</span></span>
    - <span data-ttu-id="85a7d-799">vary</span><span class="sxs-lookup"><span data-stu-id="85a7d-799">vary</span></span>
    - <span data-ttu-id="85a7d-800">via</span><span class="sxs-lookup"><span data-stu-id="85a7d-800">via</span></span>
    - <span data-ttu-id="85a7d-801">Warning</span><span class="sxs-lookup"><span data-stu-id="85a7d-801">warning</span></span>
    - <span data-ttu-id="85a7d-802">"x-ec"로 시작하는 모든 헤더 이름은 예약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-802">All header names that start with "x-ec" are reserved.</span></span>

###<a name="set-client-ip-custom-header"></a><span data-ttu-id="85a7d-803">클라이언트 IP 사용자 지정 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="85a7d-803">Set Client IP Custom Header</span></span>
<span data-ttu-id="85a7d-804">**목적:** 요청에 대한 IP 주소별로 요청 클라이언트를 식별하는 사용자 지정 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-804">**Purpose:** Adds a custom header that identifies the requesting client by IP address to the request.</span></span>

<span data-ttu-id="85a7d-805">헤더 이름 옵션은 클라이언트의 IP 주소를 저장할 사용자 지정 요청 헤더의 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-805">The Header name option defines the name of the custom request header where the client's IP address will be stored.</span></span>

<span data-ttu-id="85a7d-806">이 기능을 사용하면 고객 원본 서버에서 사용자 지정 요청 헤더를 통해 클라이언트 IP 주소를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-806">This feature allows a customer origin server to find out client IP addresses through a custom request header.</span></span> <span data-ttu-id="85a7d-807">캐시에서 요청을 제공하면 클라이언트의 IP 주소를 원본 서버에 알리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-807">If the request is served from cache, then the origin server will not be informed of the client's IP address.</span></span> <span data-ttu-id="85a7d-808">따라서 이 기능은 캐시되지 않는 ADN 또는 자산과 함께 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-808">Therefore, it is recommended that this feature be used with ADN or assets that will not be cached.</span></span>

<span data-ttu-id="85a7d-809">지정된 헤더 이름이 다음 중 하나와 일치하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-809">Please make sure that the specified header name does not match any of the following:</span></span>

- <span data-ttu-id="85a7d-810">표준 요청 헤더 이름 -</span><span class="sxs-lookup"><span data-stu-id="85a7d-810">Standard request header names.</span></span> <span data-ttu-id="85a7d-811">표준 헤더 이름 목록은 [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-811">A list of standard header names can be found in [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).</span></span>
- <span data-ttu-id="85a7d-812">예약된 헤더 이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-812">Reserved header names:</span></span>
    - <span data-ttu-id="85a7d-813">forwarded-for</span><span class="sxs-lookup"><span data-stu-id="85a7d-813">forwarded-for</span></span>
    - <span data-ttu-id="85a7d-814">host</span><span class="sxs-lookup"><span data-stu-id="85a7d-814">host</span></span>
    - <span data-ttu-id="85a7d-815">vary</span><span class="sxs-lookup"><span data-stu-id="85a7d-815">vary</span></span>
    - <span data-ttu-id="85a7d-816">via</span><span class="sxs-lookup"><span data-stu-id="85a7d-816">via</span></span>
    - <span data-ttu-id="85a7d-817">Warning</span><span class="sxs-lookup"><span data-stu-id="85a7d-817">warning</span></span>
    - <span data-ttu-id="85a7d-818">x-forwarded-for</span><span class="sxs-lookup"><span data-stu-id="85a7d-818">x-forwarded-for</span></span>
    - <span data-ttu-id="85a7d-819">"x-ec"로 시작하는 모든 헤더 이름은 예약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-819">All header names that start with "x-ec" are reserved.</span></span>
 
## <a name="logs"></a><span data-ttu-id="85a7d-820">로그</span><span class="sxs-lookup"><span data-stu-id="85a7d-820">Logs</span></span>

<span data-ttu-id="85a7d-821">이러한 기능은 원시 로그 파일에 저장된 데이터를 사용자 지정하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-821">These features are designed to customize the data stored in raw log files.</span></span>

<span data-ttu-id="85a7d-822">이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-822">Name</span></span> | <span data-ttu-id="85a7d-823">목적</span><span class="sxs-lookup"><span data-stu-id="85a7d-823">Purpose</span></span>
-----|--------
<span data-ttu-id="85a7d-824">사용자 지정 로그 필드 1</span><span class="sxs-lookup"><span data-stu-id="85a7d-824">Custom Log Field 1</span></span> | <span data-ttu-id="85a7d-825">원시 로그 파일의 사용자 지정 로그 필드에 할당할 콘텐츠와 형식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-825">Determines the format and the content that will be assigned to the custom log field in a raw log file.</span></span>
<span data-ttu-id="85a7d-826">로그 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="85a7d-826">Log Query String</span></span> | <span data-ttu-id="85a7d-827">액세스 로그에 쿼리 문자열을 URL과 함께 저장할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-827">Determines whether a query string will be stored along with the URL in access logs.</span></span>

###<a name="custom-log-field-1"></a><span data-ttu-id="85a7d-828">사용자 지정 로그 필드 1</span><span class="sxs-lookup"><span data-stu-id="85a7d-828">Custom Log Field 1</span></span>
<span data-ttu-id="85a7d-829">**목적:** 원시 로그 파일의 사용자 지정 로그 필드에 할당할 형식과 콘텐츠를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-829">**Purpose:** Determines the format and the content that will be assigned to the custom log field in a raw log file.</span></span>

<span data-ttu-id="85a7d-830">이 사용자 지정 필드는 기본적으로 로그 파일에 저장할 요청 및 응답 헤더 값을 결정할 수 있게 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-830">The main purpose behind this custom field is to allow you to determine which request and response header values will be stored in your log files.</span></span>

<span data-ttu-id="85a7d-831">기본적으로 사용자 지정 로그 필드는 "x-ec_custom-1"입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-831">By default, the custom log field is called "x-ec_custom-1."</span></span> <span data-ttu-id="85a7d-832">그러나 이 필드의 이름은 [원시 로그 설정 페이지]()에서 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-832">However, the name of this field can be customized from the [Raw Log Settings page]().</span></span>

<span data-ttu-id="85a7d-833">요청 및 응답 헤더를 지정하는 데 사용해야 하는 형식은 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-833">The formatting that you should use to specify request and response headers is defined below.</span></span>

<span data-ttu-id="85a7d-834">헤더 형식</span><span class="sxs-lookup"><span data-stu-id="85a7d-834">Header Type</span></span>|<span data-ttu-id="85a7d-835">형식</span><span class="sxs-lookup"><span data-stu-id="85a7d-835">Format</span></span>|<span data-ttu-id="85a7d-836">예</span><span class="sxs-lookup"><span data-stu-id="85a7d-836">Examples</span></span>
-|-|-
<span data-ttu-id="85a7d-837">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="85a7d-837">Request Header</span></span>|<span data-ttu-id="85a7d-838">%{[RequestHeader]()}[i]()</span><span class="sxs-lookup"><span data-stu-id="85a7d-838">%{[RequestHeader]()}[i]()</span></span> | <span data-ttu-id="85a7d-839">%{Accept-Encoding}i</span><span class="sxs-lookup"><span data-stu-id="85a7d-839">%{Accept-Encoding}i</span></span> <br/> <span data-ttu-id="85a7d-840">{Referer}i</span><span class="sxs-lookup"><span data-stu-id="85a7d-840">{Referer}i</span></span> <br/> <span data-ttu-id="85a7d-841">%{Authorization}i</span><span class="sxs-lookup"><span data-stu-id="85a7d-841">%{Authorization}i</span></span>
<span data-ttu-id="85a7d-842">응답 헤더</span><span class="sxs-lookup"><span data-stu-id="85a7d-842">Response Header</span></span>|<span data-ttu-id="85a7d-843">%{[ResponseHeader]()}[o]()</span><span class="sxs-lookup"><span data-stu-id="85a7d-843">%{[ResponseHeader]()}[o]()</span></span>| <span data-ttu-id="85a7d-844">%{Age}o</span><span class="sxs-lookup"><span data-stu-id="85a7d-844">%{Age}o</span></span> <br/> <span data-ttu-id="85a7d-845">%{Content-Type}o</span><span class="sxs-lookup"><span data-stu-id="85a7d-845">%{Content-Type}o</span></span> <br/> <span data-ttu-id="85a7d-846">%{Cookie}o</span><span class="sxs-lookup"><span data-stu-id="85a7d-846">%{Cookie}o</span></span>

<span data-ttu-id="85a7d-847">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-847">Key information:</span></span>

- <span data-ttu-id="85a7d-848">사용자 지정 로그 필드는 헤더 필드와 일반 텍스트의 조합을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-848">A custom log field can contain any combination of header fields and plain text.</span></span>
- <span data-ttu-id="85a7d-849">이 필드에 사용할 수 있는 문자는 영숫자(0-9, a-z 및 A-Z), 대시, 콜론, 세미콜론, 아포스트로피, 쉼표, 마침표, 밑줄, 등호, 괄호, 대괄호 및 공백입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-849">Valid characters for this field include the following: alphanumeric (i.e., 0-9, a-z, and A-Z), dashes, colons, semi-colons, apostrophes, commas, periods, underscores, equal signs, parentheses, brackets, and spaces.</span></span> <span data-ttu-id="85a7d-850">백분율 기호와 중괄호는 헤더 필드를 지정할 때만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-850">The percentage symbol and curly braces are only allowed when used to specify a header field.</span></span>
- <span data-ttu-id="85a7d-851">지정된 각 헤더 필드의 철자는 원하는 요청/응답 헤더 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-851">The spelling for each specified header field must match the desired request/response header name.</span></span>
- <span data-ttu-id="85a7d-852">여러 헤더를 지정하려면 구분 기호를 사용하여 각 헤더를 나타내는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-852">If you would like to specify multiple headers, then it is recommended that you use a separator to indicate each header.</span></span> <span data-ttu-id="85a7d-853">예를 들어 각 헤더에 약어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-853">For example, you could use an abbreviation for each header.</span></span> <span data-ttu-id="85a7d-854">샘플 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-854">Sample syntax is provided below.</span></span>
    - <span data-ttu-id="85a7d-855">AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o</span><span class="sxs-lookup"><span data-stu-id="85a7d-855">AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o</span></span> 

<span data-ttu-id="85a7d-856">**기본값:** -</span><span class="sxs-lookup"><span data-stu-id="85a7d-856">**Default Value:** -</span></span>

###<a name="log-query-string"></a><span data-ttu-id="85a7d-857">로그 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="85a7d-857">Log Query String</span></span>
<span data-ttu-id="85a7d-858">**목적:** 액세스 로그에 쿼리 문자열을 URL과 함께 저장할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-858">**Purpose:** Determines whether a query string will be stored along with the URL in access logs.</span></span>

<span data-ttu-id="85a7d-859">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-859">Value</span></span>|<span data-ttu-id="85a7d-860">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-860">Result</span></span>
-|-
<span data-ttu-id="85a7d-861">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-861">Enabled</span></span>|<span data-ttu-id="85a7d-862">액세스 로그에 URL을 기록할 때 쿼리 문자열을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-862">Allows the storage of query strings when recording URLs in an access log.</span></span> <span data-ttu-id="85a7d-863">URL에 쿼리 문자열이 없으면 이 옵션이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-863">If a URL does not contain a query string, then this option will not have an effect.</span></span>
<span data-ttu-id="85a7d-864">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-864">Disabled</span></span>|<span data-ttu-id="85a7d-865">기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-865">Restores the default behavior.</span></span> <span data-ttu-id="85a7d-866">기본 동작은 액세스 로그에 URL을 기록할 때 쿼리 문자열을 무시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-866">The default behavior is to ignore query strings when recording URLs in an access log.</span></span>

<span data-ttu-id="85a7d-867">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-867">**Default Behavior:** Disabled.</span></span>

<!---
## Optimize

These features determine whether a request will undergo the optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied to a request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates the Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied to a request.

If this feature has been enabled, then the following criteria must also be met before the request will be processed by Edge Optimizer:

- The requested content must use an edge CNAME URL.
- The edge CNAME referenced in the URL must correspond to a site whose configuration has been activated in a rule.

This feature requires the ADN platform and the Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that the request is eligible for Edge Optimizer processing.
Disabled|Restores the default behavior. The default behavior is to deliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates the Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and the Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests to the corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs to be performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until the Edge Optimizer – Instantiate Configuration feature that references it is removed from the rule.
- The instantiation of a site configuration does not mean that all requests to the corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If the desired site does not appear in the list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a><span data-ttu-id="85a7d-868">원본</span><span class="sxs-lookup"><span data-stu-id="85a7d-868">Origin</span></span>

<span data-ttu-id="85a7d-869">이러한 기능은 CDN이 원본 서버와 통신하는 방법을 제어하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-869">These features are designed to control how the CDN communicates with an origin server.</span></span>

<span data-ttu-id="85a7d-870">이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-870">Name</span></span> | <span data-ttu-id="85a7d-871">목적</span><span class="sxs-lookup"><span data-stu-id="85a7d-871">Purpose</span></span>
-----|--------
<span data-ttu-id="85a7d-872">최대 연결 유지 요청</span><span class="sxs-lookup"><span data-stu-id="85a7d-872">Maximum Keep-Alive Requests</span></span> | <span data-ttu-id="85a7d-873">연결이 닫히기 전에 연결을 유지할 최대 요청 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-873">Defines the maximum number of requests for a Keep-Alive connection before it is closed.</span></span>
<span data-ttu-id="85a7d-874">프록시 특별 헤더</span><span class="sxs-lookup"><span data-stu-id="85a7d-874">Proxy Special Headers</span></span> | <span data-ttu-id="85a7d-875">에지 서버에서 원본 서버로 전달할 CDN 특정 요청 헤더의 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-875">Defines the set of CDN-specific request headers that will be forwarded from an edge server to an origin server.</span></span>


###<a name="maximum-keep-alive-requests"></a><span data-ttu-id="85a7d-876">최대 연결 유지 요청</span><span class="sxs-lookup"><span data-stu-id="85a7d-876">Maximum Keep-Alive Requests</span></span>
<span data-ttu-id="85a7d-877">**목적:** 연결을 종료하기 전까지 유지할 최대 요청 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-877">**Purpose:** Defines the maximum number of requests for a Keep-Alive connection before it is closed.</span></span>

<span data-ttu-id="85a7d-878">최대 요청 수를 낮은 값으로 설정하는 것은 권장되지 않으며 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-878">Setting the maximum number of requests to a low value is strongly discouraged and may result in performance degradation.</span></span>

<span data-ttu-id="85a7d-879">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-879">Key information:</span></span>

- <span data-ttu-id="85a7d-880">이 값은 0을 포함한 양의 정수로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-880">Specify this value as a whole integer.</span></span>
- <span data-ttu-id="85a7d-881">지정된 값에 쉼표 또는 마침표를 포함하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-881">Do not include commas or periods in the specified value.</span></span>

<span data-ttu-id="85a7d-882">**기본값:** 10,000개 요청</span><span class="sxs-lookup"><span data-stu-id="85a7d-882">**Default Value:** 10,000 requests</span></span>

###<a name="proxy-special-headers"></a><span data-ttu-id="85a7d-883">프록시 특별 헤더</span><span class="sxs-lookup"><span data-stu-id="85a7d-883">Proxy Special Headers</span></span>
<span data-ttu-id="85a7d-884">**목적:** 에지 서버에서 원본 서버로 전달할 [CDN 특정 요청 헤더]() 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-884">**Purpose:** Defines the set of [CDN-specific request headers]() that will be forwarded from an edge server to an origin server.</span></span>

<span data-ttu-id="85a7d-885">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-885">Key information:</span></span>

- <span data-ttu-id="85a7d-886">이 기능에 정의된 각 CDN 특정 요청 헤더는 원본 서버로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-886">Each CDN-specific request header defined in this feature will be forwarded to an origin server.</span></span>
- <span data-ttu-id="85a7d-887">이 목록에서 CDN 특정 요청 헤더를 제거하여 이 헤더를 원본 서버로 전달하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-887">Prevent a CDN-specific request header from being forwarded to an origin server by removing it from this list.</span></span>

<span data-ttu-id="85a7d-888">**기본 동작:** 모든 [CDN 특정 요청 헤더]()를 원본 서버로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-888">**Default Behavior:** All [CDN-specific request headers]() will be forwarded to the origin server.</span></span>

## <a name="specialty"></a><span data-ttu-id="85a7d-889">특별 사항</span><span class="sxs-lookup"><span data-stu-id="85a7d-889">Specialty</span></span>

<span data-ttu-id="85a7d-890">이러한 기능은 고급 사용자만 사용해야 하는 고급 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-890">These features provide advanced functionality that should only be used by advanced users.</span></span>

<span data-ttu-id="85a7d-891">이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-891">Name</span></span> | <span data-ttu-id="85a7d-892">목적</span><span class="sxs-lookup"><span data-stu-id="85a7d-892">Purpose</span></span>
-----|--------
<span data-ttu-id="85a7d-893">캐시 가능한 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="85a7d-893">Cacheable HTTP Methods</span></span> | <span data-ttu-id="85a7d-894">네트워크에서 캐시할 수 있는 추가 HTTP 메서드 집합을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-894">Determines the set of additional HTTP methods that can be cached on our network.</span></span>
<span data-ttu-id="85a7d-895">캐시 가능한 요청 본문 크기</span><span class="sxs-lookup"><span data-stu-id="85a7d-895">Cacheable Request Body Size</span></span> | <span data-ttu-id="85a7d-896">POST 응답을 캐시할 수 있는지 여부를 결정하는 임계값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-896">Defines the threshold for determining whether a POST response can be cached.</span></span>

###<a name="cacheable-http-methods"></a><span data-ttu-id="85a7d-897">캐시 가능한 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="85a7d-897">Cacheable HTTP Methods</span></span>
<span data-ttu-id="85a7d-898">**목적:** 네트워크에서 캐시할 수 있는 추가 HTTP 메서드 집합을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-898">**Purpose:** Determines the set of additional HTTP methods that can be cached on our network.</span></span>

<span data-ttu-id="85a7d-899">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-899">Key information:</span></span>

- <span data-ttu-id="85a7d-900">이 기능은 GET 응답을 항상 캐시해야 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-900">This feature assumes that GET responses should always be cached.</span></span> <span data-ttu-id="85a7d-901">따라서 이 기능을 설정할 때 GET HTTP 메서드를 포함하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-901">As a result, the GET HTTP method should not be included when setting this feature.</span></span>
- <span data-ttu-id="85a7d-902">이 기능은 POST HTTP 메서드만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-902">This feature only supports the POST HTTP method.</span></span> <span data-ttu-id="85a7d-903">이 기능을 :POST로 설정하여 POST 응답 캐싱을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-903">Enable POST response caching by setting this feature to:POST</span></span> 
- <span data-ttu-id="85a7d-904">기본적으로 본문이 14Kb 미만인 요청만 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-904">By default, only requests whose body is smaller than 14 Kb will be cached.</span></span> <span data-ttu-id="85a7d-905">캐시 가능한 요청 본문 크기 기능을 사용하여 최대 요청 본문 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-905">Use the Cacheable Request Body Size Feature to set the maximum request body size.</span></span>

<span data-ttu-id="85a7d-906">**기본 동작:** GET 응답만 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-906">**Default Behavior:** Only GET responses will be cached.</span></span>

###<a name="cacheable-request-body-size"></a><span data-ttu-id="85a7d-907">캐시 가능한 요청 본문 크기</span><span class="sxs-lookup"><span data-stu-id="85a7d-907">Cacheable Request Body Size</span></span>

<span data-ttu-id="85a7d-908">**목적:** POST 응답을 캐시할 수 있는지 여부를 결정하는 임계값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-908">**Purpose:** Defines the threshold for determining whether a POST response can be cached.</span></span>

<span data-ttu-id="85a7d-909">이 임계값은 최대 요청 본문 크기를 지정하여 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-909">This threshold is determined by specifying a maximum request body size.</span></span> <span data-ttu-id="85a7d-910">더 큰 요청 본문을 포함한 요청은 캐시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-910">Requests that contain a larger request body will not be cached.</span></span>

<span data-ttu-id="85a7d-911">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-911">Key information:</span></span>

- <span data-ttu-id="85a7d-912">POST 응답이 캐싱에 적합한 경우에만 이 기능을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-912">This Feature is only applicable when POST responses are eligible for caching.</span></span> <span data-ttu-id="85a7d-913">캐시 가능한 HTTP 메서드 기능을 사용하여 POST 요청 캐싱을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-913">Use the Cacheable HTTP Methods Feature to enable POST request caching.</span></span>
- <span data-ttu-id="85a7d-914">요청 본문에 대한 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-914">The request body is taken into consideration for:</span></span>
    - <span data-ttu-id="85a7d-915">x-www-form-urlencoded 값</span><span class="sxs-lookup"><span data-stu-id="85a7d-915">x-www-form-urlencoded values</span></span>
    - <span data-ttu-id="85a7d-916">고유한 cache-key 보장</span><span class="sxs-lookup"><span data-stu-id="85a7d-916">Ensuring a unique cache-key</span></span>
- <span data-ttu-id="85a7d-917">최대 요청 본문 크기를 크게 정의하면 데이터 전달 성능에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-917">Defining a large maximum request body size may impact data delivery performance.</span></span>
    - <span data-ttu-id="85a7d-918">**권장되는 값:** 14Kb</span><span class="sxs-lookup"><span data-stu-id="85a7d-918">**Recommended Value:** 14 Kb</span></span>
    - <span data-ttu-id="85a7d-919">**최소값:** 1Kb</span><span class="sxs-lookup"><span data-stu-id="85a7d-919">**Minimum Value:** 1 Kb</span></span>

<span data-ttu-id="85a7d-920">**기본 동작:** 14Kb</span><span class="sxs-lookup"><span data-stu-id="85a7d-920">**Default Behavior:** 14 Kb</span></span>
 
## <a name="url"></a><span data-ttu-id="85a7d-921">URL</span><span class="sxs-lookup"><span data-stu-id="85a7d-921">URL</span></span>

<span data-ttu-id="85a7d-922">이러한 기능을 통해 요청을 다른 URL로 리디렉션하거나 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-922">These features allow a request to be redirected or rewritten to a different URL.</span></span>

<span data-ttu-id="85a7d-923">이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-923">Name</span></span> | <span data-ttu-id="85a7d-924">목적</span><span class="sxs-lookup"><span data-stu-id="85a7d-924">Purpose</span></span>
-----|--------
<span data-ttu-id="85a7d-925">리디렉션 추적</span><span class="sxs-lookup"><span data-stu-id="85a7d-925">Follow Redirects</span></span> | <span data-ttu-id="85a7d-926">고객 원본 서버에서 반환된 Location 헤더에 정의된 호스트 이름으로 요청을 리디렉션할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-926">Determines whether requests can be redirected to the hostname defined in the Location header returned by a customer origin server.</span></span>
<span data-ttu-id="85a7d-927">URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="85a7d-927">URL Redirect</span></span> | <span data-ttu-id="85a7d-928">Location 헤더를 통해 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-928">Redirects requests via the Location header.</span></span>
<span data-ttu-id="85a7d-929">URL 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-929">URL Rewrite</span></span>  | <span data-ttu-id="85a7d-930">요청 URL을 다시 씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-930">Rewrites the request URL.</span></span>

###<a name="follow-redirects"></a><span data-ttu-id="85a7d-931">리디렉션 추적</span><span class="sxs-lookup"><span data-stu-id="85a7d-931">Follow Redirects</span></span>
<span data-ttu-id="85a7d-932">**목적:** 고객 원본 서버에서 반환한 Location 헤더에 정의된 호스트 이름으로 요청을 리디렉션할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-932">**Purpose:** Determines whether requests can be redirected to the hostname defined in the Location header returned by a customer origin server.</span></span>

<span data-ttu-id="85a7d-933">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-933">Key information:</span></span>

- <span data-ttu-id="85a7d-934">요청은 동일한 플랫폼에 해당하는 에지 CNAME으로만 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-934">Requests can only be redirected to edge CNAMEs that correspond to the same platform.</span></span>

<span data-ttu-id="85a7d-935">값</span><span class="sxs-lookup"><span data-stu-id="85a7d-935">Value</span></span>|<span data-ttu-id="85a7d-936">결과</span><span class="sxs-lookup"><span data-stu-id="85a7d-936">Result</span></span>
-|-
<span data-ttu-id="85a7d-937">사용</span><span class="sxs-lookup"><span data-stu-id="85a7d-937">Enabled</span></span>|<span data-ttu-id="85a7d-938">요청을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-938">Requests can be redirected.</span></span>
<span data-ttu-id="85a7d-939">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-939">Disabled</span></span>|<span data-ttu-id="85a7d-940">요청을 리디렉션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-940">Requests will not be redirected.</span></span>

<span data-ttu-id="85a7d-941">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="85a7d-941">**Default Behavior:** Disabled.</span></span>
###<a name="url-redirect"></a><span data-ttu-id="85a7d-942">URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="85a7d-942">URL Redirect</span></span>
<span data-ttu-id="85a7d-943">**목적:** Location 헤더를 통해 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-943">**Purpose:** Redirects requests via the Location header.</span></span>

<span data-ttu-id="85a7d-944">이 기능을 구성하려면 다음 옵션을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-944">The configuration of this feature requires setting the following options:</span></span>

<span data-ttu-id="85a7d-945">옵션</span><span class="sxs-lookup"><span data-stu-id="85a7d-945">Option</span></span>|<span data-ttu-id="85a7d-946">설명</span><span class="sxs-lookup"><span data-stu-id="85a7d-946">Description</span></span>
-|-
<span data-ttu-id="85a7d-947">코드</span><span class="sxs-lookup"><span data-stu-id="85a7d-947">Code</span></span>|<span data-ttu-id="85a7d-948">요청자에게 반환할 응답 코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-948">Select the response code that will be returned to the requester.</span></span>
<span data-ttu-id="85a7d-949">원본 및 패턴</span><span class="sxs-lookup"><span data-stu-id="85a7d-949">Source & Pattern</span></span>| <span data-ttu-id="85a7d-950">이러한 설정은 리디렉션될 수 있는 요청의 형식을 식별하는 요청 URI 패턴을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-950">These settings define a request URI pattern that identifies the type of requests that may be redirected.</span></span> <span data-ttu-id="85a7d-951">URL이 다음 기준을 모두 충족하는 요청만 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-951">Only requests whose URL satisfies both of the following criteria will be redirected:</span></span> <br/> <br/> <span data-ttu-id="85a7d-952">**원본:**(또는 콘텐츠 액세스 지점) 원본 서버를 식별하는 상대 경로를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-952">**Source :** (or content access point) Select a relative path that identifies an origin server.</span></span> <span data-ttu-id="85a7d-953">이는 "/XXXX/" 섹션과 끝점 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-953">This is the  "/XXXX/" section and your endpoint name.</span></span> <br/> <span data-ttu-id="85a7d-954">**원본(패턴):** 상대 경로로 요청을 식별하는 패턴을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-954">**Source (pattern):** A pattern that identifies requests by relative path must be defined.</span></span> <span data-ttu-id="85a7d-955">이 정규식 패턴은 이전에 선택한 콘텐츠 액세스 지점 바로 뒤에서 시작하는 경로를 정의해야 합니다(위 참조).</span><span class="sxs-lookup"><span data-stu-id="85a7d-955">This regular expression pattern must define a path that starts directly after the previously selected content access point (see above).</span></span> <br/> <span data-ttu-id="85a7d-956">- 위에서 정의한 요청 URI 기준(즉, 원본 및 패턴)이 이 기능에 대해 정의된 일치 조건과 충돌하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-956">- Make sure that the request URI criteria (i.e., Source & Pattern) defined above doesn't conflict with any match conditions defined for this feature.</span></span> <br/> <span data-ttu-id="85a7d-957">- 패턴을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-957">- Make sure to specify a pattern.</span></span> <span data-ttu-id="85a7d-958">빈 값을 패턴으로 사용하면 선택한 원본 서버의 루트 폴더(예: http://cdn.mydomain.com/)에 대한 요청만 일치하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-958">Using a blank value as the pattern will only match requests to the root folder of the selected origin server (e.g., http://cdn.mydomain.com/).</span></span>
<span data-ttu-id="85a7d-959">대상</span><span class="sxs-lookup"><span data-stu-id="85a7d-959">Destination</span></span>| <span data-ttu-id="85a7d-960">위의 요청을 리디렉션할 URL을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-960">Define the URL to which the above requests will be redirected.</span></span> <br/> <span data-ttu-id="85a7d-961">다음을 사용하여 이 URL을 동적으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-961">Dynamically construct this URL using:</span></span> <br/> <span data-ttu-id="85a7d-962">- 정규식 패턴</span><span class="sxs-lookup"><span data-stu-id="85a7d-962">- A regular expression pattern</span></span> <br/><span data-ttu-id="85a7d-963">- HTTP 변수</span><span class="sxs-lookup"><span data-stu-id="85a7d-963">- HTTP variables</span></span> <br/> <span data-ttu-id="85a7d-964">$를 사용 하 여 대상 패턴에는 소스 패턴에서 캡처된 값으로 대체_ n _ 여기서 _ n _ 캡처되는 순서에 따라 값을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-964">Substitute the values captured in the source pattern into the destination pattern using $_n_ where _n_ identifies a value by the order in which it was captured.</span></span> <span data-ttu-id="85a7d-965">예를 들어 $1은 원본 패턴에서 캡처한 첫 번째 값을 나타내고, $2는 두 번째 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-965">For example, $1 represents the first value captured in the source pattern, while $2 represents the second value.</span></span> <br/> 
<span data-ttu-id="85a7d-966">절대 URL을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-966">It is highly recommended to use an absolute URL.</span></span> <span data-ttu-id="85a7d-967">상대 URL을 사용하면 CDN URL을 잘못된 경로로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-967">The use of a relative URL may redirect CDN URLs to an invalid path.</span></span>

<span data-ttu-id="85a7d-968">**샘플 시나리오**</span><span class="sxs-lookup"><span data-stu-id="85a7d-968">**Sample Scenario**</span></span>

<span data-ttu-id="85a7d-969">이 예제에서는 기본 CDN URL(http://marketing.azureedge.net/brochures)로 확인되는 에지 CNAME URL을 리디렉션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-969">In this example, we will demonstrate how to redirect an edge CNAME URL that resolves to this base CDN URL: http://marketing.azureedge.net/brochures</span></span>

<span data-ttu-id="85a7d-970">요청이 유효하면 기본 에지 CNAME URL(http://cdn.mydomain.com/resources)으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-970">Qualifying requests will be redirected to this base edge CNAME URL: http://cdn.mydomain.com/resources</span></span>

<span data-ttu-id="85a7d-971">이 URL 리디렉션은 다음 구성을 통해 수행할 수 있습니다. ![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)</span><span class="sxs-lookup"><span data-stu-id="85a7d-971">This URL redirection may be achieved through the following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)</span></span>

<span data-ttu-id="85a7d-972">**주요 정보:**</span><span class="sxs-lookup"><span data-stu-id="85a7d-972">**Key points:**</span></span>

- <span data-ttu-id="85a7d-973">URL 리디렉션 기능은 리디렉션할 요청 URL을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-973">The URL Redirect feature defines the request URLs that will be redirected.</span></span> <span data-ttu-id="85a7d-974">따라서 추가적인 일치 조건이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-974">As a result, additional match conditions are not required.</span></span> <span data-ttu-id="85a7d-975">일치 조건을 "Always"로 정의했지만 "marketing" 고객 원본의 "brochures" 폴더를 가리키는 요청만 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-975">Although the match condition was defined as "Always," only requests that point to the "brochures" folder on the "marketing" customer origin will be redirected.</span></span> 
- <span data-ttu-id="85a7d-976">일치하는 모든 요청은 대상 옵션에 정의된 에지 CNAME URL로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-976">All matching requests will be redirected to the edge CNAME URL defined in the Destination option.</span></span> 
    - <span data-ttu-id="85a7d-977">샘플 시나리오 #1:</span><span class="sxs-lookup"><span data-stu-id="85a7d-977">Sample scenario #1:</span></span> 
        - <span data-ttu-id="85a7d-978">샘플 요청(CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="85a7d-978">Sample request (CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf</span></span> 
        - <span data-ttu-id="85a7d-979">요청 URL(리디렉션 이후): http://cdn.mydomain.com/resources/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="85a7d-979">Request URL (after redirect): http://cdn.mydomain.com/resources/widgets.pdf</span></span>  
    - <span data-ttu-id="85a7d-980">샘플 시나리오 2:</span><span class="sxs-lookup"><span data-stu-id="85a7d-980">Sample scenario #2:</span></span> 
        - <span data-ttu-id="85a7d-981">샘플 요청(에지 CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="85a7d-981">Sample request (Edge CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf</span></span> 
        - <span data-ttu-id="85a7d-982">요청 URL(리디렉션 이후): http://cdn.mydomain.com/resources/widgets.pdf 샘플 시나리오</span><span class="sxs-lookup"><span data-stu-id="85a7d-982">Request URL (after redirect): http://cdn.mydomain.com/resources/widgets.pdf  Sample scenario</span></span>
    - <span data-ttu-id="85a7d-983">샘플 시나리오 #3:</span><span class="sxs-lookup"><span data-stu-id="85a7d-983">Sample scenario #3:</span></span> 
        - <span data-ttu-id="85a7d-984">샘플 요청(에지 CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt</span><span class="sxs-lookup"><span data-stu-id="85a7d-984">Sample request (Edge CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt</span></span> 
        - <span data-ttu-id="85a7d-985">요청 URL(리디렉션 이후):: http://cdn.mydomain.com/resources/campaignA/final/productC.ppt</span><span class="sxs-lookup"><span data-stu-id="85a7d-985">Request URL (after redirect): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt</span></span>  
- <span data-ttu-id="85a7d-986">요청 스키마(%{scheme}) 변수는 대상 옵션에서 활용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-986">The Request Scheme (%{scheme}) variable was leveraged in the Destination option.</span></span> <span data-ttu-id="85a7d-987">이렇게 하면 리디렉션 후에도 요청의 스키마가 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-987">This ensures that the request's scheme remains unchanged after redirection.</span></span>
- <span data-ttu-id="85a7d-988">요청에서 캡처한 URL 세그먼트는 "$1"을 통해 새 URL에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-988">The URL segments that were captured from the request are appended to the new URL via "$1."</span></span>
 
###<a name="url-rewrite"></a><span data-ttu-id="85a7d-989">URL 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="85a7d-989">URL Rewrite</span></span>
<span data-ttu-id="85a7d-990">**목적:** 요청 URL을 다시 씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-990">**Purpose:** Rewrites the request URL.</span></span>

<span data-ttu-id="85a7d-991">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="85a7d-991">Key information:</span></span>

- <span data-ttu-id="85a7d-992">이 기능을 구성하려면 다음 옵션을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-992">The configuration of this feature requires setting the following options:</span></span>

<span data-ttu-id="85a7d-993">옵션</span><span class="sxs-lookup"><span data-stu-id="85a7d-993">Option</span></span>|<span data-ttu-id="85a7d-994">설명</span><span class="sxs-lookup"><span data-stu-id="85a7d-994">Description</span></span>
-|-
 <span data-ttu-id="85a7d-995">원본 및 패턴</span><span class="sxs-lookup"><span data-stu-id="85a7d-995">Source & Pattern</span></span> | <span data-ttu-id="85a7d-996">이러한 설정은 다시 쓸 수 있는 요청의 형식을 식별하는 요청 URI 패턴을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-996">These settings define a request URI pattern that identifies the type of requests that may be rewritten.</span></span> <span data-ttu-id="85a7d-997">URL이 다음 기준을 모두 충족하는 요청만 다시 씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-997">Only requests whose URL satisfies both of the following criteria will be rewritten:</span></span> <br/>     <span data-ttu-id="85a7d-998">- **원본(또는 콘텐츠 액세스 지점):** 원본 서버를 식별하는 상대 경로를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-998">- **Source (or content access point):** Select a relative path that identifies an origin server.</span></span> <span data-ttu-id="85a7d-999">이는 "/XXXX/" 섹션과 끝점 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-999">This is the  "/XXXX/" section and your endpoint name.</span></span> <br/> <span data-ttu-id="85a7d-1000">- **원본(패턴):** 상대 경로로 요청을 식별하는 패턴을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1000">- **Source (pattern):** A pattern that identifies requests by relative path must be defined.</span></span> <span data-ttu-id="85a7d-1001">이 정규식 패턴은 이전에 선택한 콘텐츠 액세스 지점 바로 뒤에서 시작하는 경로를 정의해야 합니다(위 참조).</span><span class="sxs-lookup"><span data-stu-id="85a7d-1001">This regular expression pattern must define a path that starts directly after the previously selected content access point (see above).</span></span> <br/> <span data-ttu-id="85a7d-1002">위에서 정의한 요청 URI 기준(즉, 원본 및 패턴)이 이 기능에 대해 정의된 일치 조건과 충돌하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1002">Make sure that the request URI criteria (i.e., Source & Pattern) defined above doesn't conflict with any of the match conditions defined for this feature.</span></span> <span data-ttu-id="85a7d-1003">패턴을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1003">Make sure to specify a pattern.</span></span> <span data-ttu-id="85a7d-1004">빈 값을 패턴으로 사용하면 선택한 원본 서버의 루트 폴더(예: http://cdn.mydomain.com/)에 대한 요청만 일치하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1004">Using a blank value as the pattern will only match requests to the root folder of the selected origin server (e.g., http://cdn.mydomain.com/).</span></span> 
 <span data-ttu-id="85a7d-1005">대상</span><span class="sxs-lookup"><span data-stu-id="85a7d-1005">Destination</span></span>  |<span data-ttu-id="85a7d-1006">위의 요청을 다시 쓸 상대 URL을 다음과 같이 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1006">Define the relative URL to which the above requests will be rewritten by:</span></span> <br/>    <span data-ttu-id="85a7d-1007">1. 원본 서버를 식별하는 콘텐츠 액세스 지점 선택</span><span class="sxs-lookup"><span data-stu-id="85a7d-1007">1. Selecting a content access point that identifies an origin server.</span></span> <br/>    <span data-ttu-id="85a7d-1008">2. 다음을 사용하여 상대 경로 정의</span><span class="sxs-lookup"><span data-stu-id="85a7d-1008">2. Defining a relative path using:</span></span> <br/>        <span data-ttu-id="85a7d-1009">- 정규식 패턴</span><span class="sxs-lookup"><span data-stu-id="85a7d-1009">- A regular expression pattern</span></span> <br/>        <span data-ttu-id="85a7d-1010">- HTTP 변수</span><span class="sxs-lookup"><span data-stu-id="85a7d-1010">- HTTP variables</span></span> <br/> <br/> <span data-ttu-id="85a7d-1011">$를 사용 하 여 대상 패턴에는 소스 패턴에서 캡처된 값으로 대체_ n _ 여기서 _ n _ 캡처되는 순서에 따라 값을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1011">Substitute the values captured in the source pattern into the destination pattern using $_n_ where _n_ identifies a value by the order in which it was captured.</span></span> <span data-ttu-id="85a7d-1012">예를 들어 $1은 원본 패턴에서 캡처한 첫 번째 값을 나타내고, $2는 두 번째 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1012">For example, $1 represents the first value captured in the source pattern, while $2 represents the second value.</span></span> 
 <span data-ttu-id="85a7d-1013">이 기능을 사용하면 에지 서버에서 기존의 리디렉션을 수행하지 않고도 URL을 다시 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1013">This feature allows our edge servers to rewrite the URL without performing a traditional redirect.</span></span> <span data-ttu-id="85a7d-1014">즉 요청자가 다시 쓴 URL을 요청한 것과 동일한 응답 코드를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1014">This means that the requester will receive the same response code as if the rewritten URL had been requested.</span></span>

<span data-ttu-id="85a7d-1015">**샘플 시나리오 1**</span><span class="sxs-lookup"><span data-stu-id="85a7d-1015">**Sample Scenario 1**</span></span>

<span data-ttu-id="85a7d-1016">이 예제에서는 기본 CDN URL(http://marketing.azureedge.net/brochures)로 확인되는 에지 CNAME URL을 리디렉션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1016">In this example, we will demonstrate how to redirect an edge CNAME URL that resolves to this base CDN URL: http://marketing.azureedge.net/brochures/</span></span>

<span data-ttu-id="85a7d-1017">요청이 유효하면 기본 에지 CNAME URL(http://MyOrigin.azureedge.net/resources/)으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1017">Qualifying requests will be redirected to this base edge CNAME URL: http://MyOrigin.azureedge.net/resources/</span></span>

<span data-ttu-id="85a7d-1018">이 URL 리디렉션은 다음 구성을 통해 수행할 수 있습니다. ![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)</span><span class="sxs-lookup"><span data-stu-id="85a7d-1018">This URL redirection may be achieved through the following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)</span></span>

<span data-ttu-id="85a7d-1019">**샘플 시나리오 2**</span><span class="sxs-lookup"><span data-stu-id="85a7d-1019">**Sample Scenario 2**</span></span>

<span data-ttu-id="85a7d-1020">이 예제에서는 정규식을 사용하여 에지 CNAME URL을 대문자에서 소문자로 리디렉션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1020">In this example, we will demonstrate how to redirect an edge CNAME URL from UPPERCASE to lowercase using regular expressions.</span></span>

<span data-ttu-id="85a7d-1021">이 URL 리디렉션은 다음 구성을 통해 수행할 수 있습니다. ![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)</span><span class="sxs-lookup"><span data-stu-id="85a7d-1021">This URL redirection may be achieved through the following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)</span></span>


<span data-ttu-id="85a7d-1022">**주요 정보:**</span><span class="sxs-lookup"><span data-stu-id="85a7d-1022">**Key points:**</span></span>

- <span data-ttu-id="85a7d-1023">URL 다시 쓰기 기능은 다시 쓸 요청 URL을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1023">The URL Rewrite feature defines the request URLs that will be rewritten.</span></span> <span data-ttu-id="85a7d-1024">따라서 추가적인 일치 조건이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1024">As a result, additional match conditions are not required.</span></span> <span data-ttu-id="85a7d-1025">일치 조건을 "Always"로 정의했지만 "marketing" 고객 원본의 "brochures" 폴더를 가리키는 요청만 다시 씁니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1025">Although the match condition was defined as "Always," only requests that point to the "brochures" folder on the "marketing" customer origin will be rewritten.</span></span>

- <span data-ttu-id="85a7d-1026">요청에서 캡처한 URL 세그먼트는 "$1"을 통해 새 URL에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1026">The URL segments that were captured from the request are appended to the new URL via "$1."</span></span>



###<a name="compatibility"></a><span data-ttu-id="85a7d-1027">호환성</span><span class="sxs-lookup"><span data-stu-id="85a7d-1027">Compatibility</span></span>

<span data-ttu-id="85a7d-1028">이 기능에는 요청에 적용하기 전에 충족되어야 하는 일치 조건이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1028">This feature includes matching criteria that must be met before it can be applied to a request.</span></span> <span data-ttu-id="85a7d-1029">충돌하는 일치 기준을 설정하지 않도록 방지하기 위해 이 기능은 다음 일치 조건과 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85a7d-1029">In order to prevent setting up conflicting match criteria, this feature is incompatible with the following match conditions:</span></span>

- <span data-ttu-id="85a7d-1030">AS 숫자</span><span class="sxs-lookup"><span data-stu-id="85a7d-1030">AS Number</span></span>
- <span data-ttu-id="85a7d-1031">CDN 원본</span><span class="sxs-lookup"><span data-stu-id="85a7d-1031">CDN Origin</span></span>
- <span data-ttu-id="85a7d-1032">클라이언트 IP 주소</span><span class="sxs-lookup"><span data-stu-id="85a7d-1032">Client IP Address</span></span>
- <span data-ttu-id="85a7d-1033">고객 원본</span><span class="sxs-lookup"><span data-stu-id="85a7d-1033">Customer Origin</span></span>
- <span data-ttu-id="85a7d-1034">요청 스키마</span><span class="sxs-lookup"><span data-stu-id="85a7d-1034">Request Scheme</span></span>
- <span data-ttu-id="85a7d-1035">URL 경로 디렉터리</span><span class="sxs-lookup"><span data-stu-id="85a7d-1035">URL Path Directory</span></span>
- <span data-ttu-id="85a7d-1036">URL 경로 확장</span><span class="sxs-lookup"><span data-stu-id="85a7d-1036">URL Path Extension</span></span>
- <span data-ttu-id="85a7d-1037">URL 경로 파일 이름</span><span class="sxs-lookup"><span data-stu-id="85a7d-1037">URL Path Filename</span></span>
- <span data-ttu-id="85a7d-1038">URL 경로 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-1038">URL Path Literal</span></span>
- <span data-ttu-id="85a7d-1039">URL 경로 Regex</span><span class="sxs-lookup"><span data-stu-id="85a7d-1039">URL Path Regex</span></span>
- <span data-ttu-id="85a7d-1040">URL 경로 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-1040">URL Path Wildcard</span></span>
- <span data-ttu-id="85a7d-1041">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="85a7d-1041">URL Query Literal</span></span>
- <span data-ttu-id="85a7d-1042">URL 쿼리 매개 변수</span><span class="sxs-lookup"><span data-stu-id="85a7d-1042">URL Query Parameter</span></span>
- <span data-ttu-id="85a7d-1043">URL 쿼리 Regex</span><span class="sxs-lookup"><span data-stu-id="85a7d-1043">URL Query Regex</span></span>
- <span data-ttu-id="85a7d-1044">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="85a7d-1044">URL Query Wildcard</span></span>


## <a name="next-steps"></a><span data-ttu-id="85a7d-1045">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85a7d-1045">Next Steps</span></span>
* [<span data-ttu-id="85a7d-1046">규칙 엔진 참조</span><span class="sxs-lookup"><span data-stu-id="85a7d-1046">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="85a7d-1047">규칙 엔진 조건식</span><span class="sxs-lookup"><span data-stu-id="85a7d-1047">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="85a7d-1048">규칙 엔진 일치 조건</span><span class="sxs-lookup"><span data-stu-id="85a7d-1048">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="85a7d-1049">규칙 엔진을 사용하여 기본 HTTP 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="85a7d-1049">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* [<span data-ttu-id="85a7d-1050">Azure CDN 개요</span><span class="sxs-lookup"><span data-stu-id="85a7d-1050">Azure CDN Overview</span></span>](cdn-overview.md)
