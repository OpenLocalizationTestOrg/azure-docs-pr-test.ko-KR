---
title: "CDN aaaAzure 규칙 엔진 기능 | Microsoft Docs"
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
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a><span data-ttu-id="18385-103">Azure CDN 규칙 엔진 기능</span><span class="sxs-lookup"><span data-stu-id="18385-103">Azure CDN rules engine features</span></span>
<span data-ttu-id="18385-104">이 항목에 자세히 설명 hello 사용할 수 있는 기능에 대 한 Azure 네트워크 CDN (콘텐츠 배달)에서는 [규칙 엔진](cdn-rules-engine.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-104">This topic lists detailed descriptions of hello available features for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="18385-105">규칙의 세 번째 부분 hello는 hello 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-105">hello third part of a rule is hello feature.</span></span> <span data-ttu-id="18385-106">수 있는 작업의 hello 형식을 정의 하는 기능 toohello 유형의 집합 일치 조건에 의해 식별 되는 요청을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-106">A feature defines hello type of action that will be applied toohello type of request identified by a set of match conditions.</span></span>

## <a name="access"></a><span data-ttu-id="18385-107">Access</span><span class="sxs-lookup"><span data-stu-id="18385-107">Access</span></span>

<span data-ttu-id="18385-108">이러한 기능은 디자인 된 toocontrol 액세스 toocontent 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-108">These features are designed toocontrol access toocontent.</span></span>


<span data-ttu-id="18385-109">이름</span><span class="sxs-lookup"><span data-stu-id="18385-109">Name</span></span> | <span data-ttu-id="18385-110">목적</span><span class="sxs-lookup"><span data-stu-id="18385-110">Purpose</span></span>
-----|--------
<span data-ttu-id="18385-111">액세스 거부</span><span class="sxs-lookup"><span data-stu-id="18385-111">Deny Access</span></span> | <span data-ttu-id="18385-112">모든 요청이 403 사용 권한 없음 응답으로 거부되는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-112">Determines whether all requests are rejected with a 403 Forbidden response.</span></span>
<span data-ttu-id="18385-113">토큰 인증</span><span class="sxs-lookup"><span data-stu-id="18385-113">Token Auth</span></span> | <span data-ttu-id="18385-114">토큰 기반 인증 적용된 tooa 요청 않을 것인지를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-114">Determines whether Token-Based Authentication will be applied tooa request.</span></span>
<span data-ttu-id="18385-115">토큰 인증 거부 코드</span><span class="sxs-lookup"><span data-stu-id="18385-115">Token Auth Denial Code</span></span> | <span data-ttu-id="18385-116">반환 되는 tooa 사용자 요청이 거부 되는 tooToken 기반 인증 인 경우 응답의 hello 유형을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-116">Determines hello type of response that will be returned tooa user when a request is denied due tooToken-Based Authentication.</span></span>
<span data-ttu-id="18385-117">토큰 인증 URL 대/소문자 무시</span><span class="sxs-lookup"><span data-stu-id="18385-117">Token Auth Ignore URL Case</span></span> | <span data-ttu-id="18385-118">토큰 기반 인증에서 URL 비교 시 대/소문자를 구분할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-118">Determines whether URL comparisons made by Token-Based Authentication will be case-sensitive.</span></span>
<span data-ttu-id="18385-119">토큰 인증 매개 변수</span><span class="sxs-lookup"><span data-stu-id="18385-119">Token Auth Parameter</span></span> | <span data-ttu-id="18385-120">Hello 토큰 기반 인증 쿼리 문자열 매개 변수 이름을 바꿔야 하는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-120">Determines whether hello Token-Based Authentication query string parameter should be renamed.</span></span>

### <a name="deny-access"></a><span data-ttu-id="18385-121">액세스 거부</span><span class="sxs-lookup"><span data-stu-id="18385-121">Deny Access</span></span>
<span data-ttu-id="18385-122">**목적**: 모든 요청이 403 사용할 수 없음 응답으로 거부되는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-122">**Purpose**: Determines whether all requests are rejected with a 403 Forbidden response.</span></span>

<span data-ttu-id="18385-123">값</span><span class="sxs-lookup"><span data-stu-id="18385-123">Value</span></span> | <span data-ttu-id="18385-124">결과</span><span class="sxs-lookup"><span data-stu-id="18385-124">Result</span></span>
------|-------
<span data-ttu-id="18385-125">사용</span><span class="sxs-lookup"><span data-stu-id="18385-125">Enabled</span></span>| <span data-ttu-id="18385-126">Hello 일치 하는 조건을 toobe 403 사용 권한 없음 응답와 함께 거부를 만족 하는 모든 요청 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-126">Causes all requests that satisfy hello matching criteria toobe rejected with a 403 Forbidden response.</span></span>
<span data-ttu-id="18385-127">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-127">Disabled</span></span>| <span data-ttu-id="18385-128">Hello 기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-128">Restores hello default behavior.</span></span> <span data-ttu-id="18385-129">hello 기본 동작은 tooallow hello 원본 toodetermine hello의 서버 유형을 반환 되는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-129">hello default behavior is tooallow hello origin server toodetermine hello type of response that will be returned.</span></span>

<span data-ttu-id="18385-130">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-130">**Default Behavior**: Disabled</span></span>

> [!TIP]
   > <span data-ttu-id="18385-131">이 기능은 사용할 수는 tooassociate 조건 tooblock 액세스 tooHTTP 참조 페이지 인라인 링크 tooyour 콘텐츠를 사용 하는 요청 헤더와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-131">One possible use for this feature is tooassociate it with a Request Header match condition tooblock access tooHTTP referrers that are using inline links tooyour content.</span></span>

### <a name="token-auth"></a><span data-ttu-id="18385-132">토큰 인증</span><span class="sxs-lookup"><span data-stu-id="18385-132">Token Auth</span></span>
<span data-ttu-id="18385-133">**목적:** 토큰 기반 인증 적용된 tooa 요청 않을 것인지를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-133">**Purpose:** Determines whether Token-Based Authentication will be applied tooa request.</span></span>

<span data-ttu-id="18385-134">토큰 기반 인증을 사용 하는 경우 암호화 된 토큰을 제공 하 고 해당 토큰이 지정 된 toohello 요구 사항을 준수 하는 유일한 요청 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-134">If Token-Based Authentication is enabled, then only requests that provide an encrypted token and comply toohello requirements specified by that token will be honored.</span></span>

<span data-ttu-id="18385-135">hello 한 암호화 키를 사용 하는 tooencrypt 및 암호 해독 토큰 값이 됩니다는 기본 키와 토큰 인증 페이지의 키 백업 옵션에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-135">hello encryption key that will be used tooencrypt and decrypt token values is determined by the Primary Key and the Backup Key options on the Token Auth page.</span></span> <span data-ttu-id="18385-136">암호화 키는 플랫폼에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="18385-136">Keep in mind that encryption keys are platform-specific.</span></span>

<span data-ttu-id="18385-137">값</span><span class="sxs-lookup"><span data-stu-id="18385-137">Value</span></span> | <span data-ttu-id="18385-138">결과</span><span class="sxs-lookup"><span data-stu-id="18385-138">Result</span></span>
------|---------
<span data-ttu-id="18385-139">사용</span><span class="sxs-lookup"><span data-stu-id="18385-139">Enabled</span></span> | <span data-ttu-id="18385-140">보호 hello 토큰 기반 인증을 사용 하는 콘텐츠를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-140">Protects hello requested content with Token-Based Authentication.</span></span> <span data-ttu-id="18385-141">유효한 토큰을 제공하고 요구 사항을 충족하는 클라이언트의 요청만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-141">Only requests from clients that provide a valid token and meet its requirements will be honored.</span></span> <span data-ttu-id="18385-142">FTP 트랜잭션은 토큰 기반 인증에서 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-142">FTP transactions are excluded from Token-Based Authentication.</span></span>
<span data-ttu-id="18385-143">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-143">Disabled</span></span>| <span data-ttu-id="18385-144">Hello 기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-144">Restores hello default behavior.</span></span> <span data-ttu-id="18385-145">기본 동작은 hello가 tooallow 토큰 기반 인증 구성 toodetermine 요청은 보안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-145">hello default behavior is tooallow your Token-Based Authentication configuration toodetermine whether a request will be secured.</span></span>

<span data-ttu-id="18385-146">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-146">**Default Behavior:** Disabled.</span></span>

###<a name="token-auth-denial-code"></a><span data-ttu-id="18385-147">토큰 인증 거부 코드</span><span class="sxs-lookup"><span data-stu-id="18385-147">Token Auth Denial Code</span></span>
<span data-ttu-id="18385-148">**목적:** 반환 되는 tooa 사용자 요청이 거부 되는 tooToken 기반 인증 인 경우 응답의 hello 유형을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-148">**Purpose:** Determines hello type of response that will be returned tooa user when a request is denied due tooToken-Based Authentication.</span></span>

<span data-ttu-id="18385-149">hello 사용할 수 있는 응답 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-149">hello available response codes are listed below.</span></span>

<span data-ttu-id="18385-150">응답 코드</span><span class="sxs-lookup"><span data-stu-id="18385-150">Response Code</span></span>|<span data-ttu-id="18385-151">응답 이름</span><span class="sxs-lookup"><span data-stu-id="18385-151">Response Name</span></span>|<span data-ttu-id="18385-152">설명</span><span class="sxs-lookup"><span data-stu-id="18385-152">Description</span></span>
----------------|-----------|--------
<span data-ttu-id="18385-153">301</span><span class="sxs-lookup"><span data-stu-id="18385-153">301</span></span>|<span data-ttu-id="18385-154">영구적으로 이동됨</span><span class="sxs-lookup"><span data-stu-id="18385-154">Moved Permanently</span></span>|<span data-ttu-id="18385-155">이 상태 코드의 위치 헤더에 지정 된 권한이 없는 사용자가 toohello URL로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-155">This status code redirects unauthorized users toohello URL specified in the Location header.</span></span>
<span data-ttu-id="18385-156">302</span><span class="sxs-lookup"><span data-stu-id="18385-156">302</span></span>|<span data-ttu-id="18385-157">있음</span><span class="sxs-lookup"><span data-stu-id="18385-157">Found</span></span>|<span data-ttu-id="18385-158">이 상태 코드의 위치 헤더에 지정 된 권한이 없는 사용자가 toohello URL로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-158">This status code redirects unauthorized users toohello URL specified in the Location header.</span></span> <span data-ttu-id="18385-159">이 상태 코드는 hello 산업 표준 방법의 리디렉션을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-159">This status code is hello industry standard method of performing a redirect.</span></span>
<span data-ttu-id="18385-160">307</span><span class="sxs-lookup"><span data-stu-id="18385-160">307</span></span>|<span data-ttu-id="18385-161">임시 리디렉션</span><span class="sxs-lookup"><span data-stu-id="18385-161">Temporary Redirect</span></span>|<span data-ttu-id="18385-162">이 상태 코드의 위치 헤더에 지정 된 권한이 없는 사용자가 toohello URL로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-162">This status code redirects unauthorized users toohello URL specified in the Location header.</span></span>
<span data-ttu-id="18385-163">401</span><span class="sxs-lookup"><span data-stu-id="18385-163">401</span></span>|<span data-ttu-id="18385-164">권한 없음</span><span class="sxs-lookup"><span data-stu-id="18385-164">Unauthorized</span></span>|<span data-ttu-id="18385-165">이 상태 코드를 응답 Www-authenticate 헤더 함께 사용 하면 사용자에 게 인증 tooprompt이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-165">Combining this status code with the WWW-Authenticate response header allows you tooprompt a user for authentication.</span></span>
<span data-ttu-id="18385-166">403</span><span class="sxs-lookup"><span data-stu-id="18385-166">403</span></span>|<span data-ttu-id="18385-167">사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="18385-167">Forbidden</span></span>|<span data-ttu-id="18385-168">이 hello 표준 403 사용할 수 없음 상태 메시지 콘텐츠 보호 tooaccess 시도 때 권한 없는 사용자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-168">This is hello standard 403 Forbidden status message that an unauthorized user will see when trying tooaccess protected content.</span></span>
<span data-ttu-id="18385-169">404</span><span class="sxs-lookup"><span data-stu-id="18385-169">404</span></span>|<span data-ttu-id="18385-170">파일을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="18385-170">File Not Found</span></span>|<span data-ttu-id="18385-171">이 상태 코드는 hello HTTP 클라이언트 hello 서버와 수 toocommunicate 있지만 hello 요청한 콘텐츠를 찾을 수 없습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18385-171">This status code indicates that hello HTTP client was able toocommunicate with hello server, but hello requested content was not found.</span></span>

#### <a name="url-redirection"></a><span data-ttu-id="18385-172">URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="18385-172">URL Redirection</span></span>

<span data-ttu-id="18385-173">이 기능은 구성 된 tooreturn 3xx 상태 코드 되었을 때 URL 리디렉션 tooa 사용자 지정 URL을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-173">This feature supports URL redirection tooa user-defined URL when it is configured tooreturn a 3xx status code.</span></span> <span data-ttu-id="18385-174">Hello 다음 단계를 수행 하 여이 사용자 지정 URL은 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-174">This user-defined URL can be specified by performing hello following steps:</span></span>

1. <span data-ttu-id="18385-175">Hello 토큰 인증 거부 코드 기능에 대 한 3xx 응답 코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-175">Select a 3xx response code for hello Token Auth Denial Code feature.</span></span>
2. <span data-ttu-id="18385-176">선택적 헤더 이름 옵션에서 "Location"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-176">Select "Location" from the Optional Header Name option.</span></span>
3. <span data-ttu-id="18385-177">선택적 헤더 값 옵션 toohello 필요한 URL을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-177">Set the Optional Header Value option toohello desired URL.</span></span>

<span data-ttu-id="18385-178">URL 3xx 상태 코드를 정의 하지 않은 경우 다음 hello 3xx 상태 코드에 대 한 표준 응답 페이지가 반환할 toohello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-178">If a URL is not defined for a 3xx status code, then hello standard response page for a 3xx status code will be returned toohello user.</span></span>

<span data-ttu-id="18385-179">URL 리디렉션은 3xx 응답 코드에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-179">URL redirection is only applicable for 3xx response codes.</span></span>

<span data-ttu-id="18385-180">선택적 헤더 값 옵션은 영숫자, 인용 부호 및 공백을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-180">The Optional Header Value option supports alphanumeric characters, quotation marks, and spaces.</span></span>

#### <a name="authentication"></a><span data-ttu-id="18385-181">인증</span><span class="sxs-lookup"><span data-stu-id="18385-181">Authentication</span></span>

<span data-ttu-id="18385-182">이 기능은 tooan 토큰 기반 인증으로 보호 된 콘텐츠에 대 한 권한이 없는 요청에 응답할 때 hello 기능 tooinclude WWW 인증 헤더를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-182">This feature supports hello capability tooinclude the WWW-Authenticate header when responding tooan unauthorized request for content protected by Token-Based Authentication.</span></span> <span data-ttu-id="18385-183">Www-authenticate 헤더에 설정 된 경우 구성에서 너무 "기본" hello 권한이 없는 사용자 계정 자격 증명에 대 한 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="18385-183">If the WWW-Authenticate header has been set too"basic" in your configuration, then hello unauthorized user will be prompted for account credentials.</span></span>

<span data-ttu-id="18385-184">구성 이상 hello hello 다음 단계를 수행 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-184">hello above configuration can be achieved by performing hello following steps:</span></span>

1. <span data-ttu-id="18385-185">Hello 토큰 인증 거부 코드 기능에 대 한 hello 응답 코드와 "401"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-185">Select "401" as hello response code for hello Token Auth Denial Code feature.</span></span>
2. <span data-ttu-id="18385-186">선택적 헤더 이름 옵션에서 "WWW-Authenticate"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-186">Select "WWW-Authenticate" from the Optional Header Name option.</span></span>
3. <span data-ttu-id="18385-187">선택적 헤더 값 옵션이 너무 "기본 설정 합니다."</span><span class="sxs-lookup"><span data-stu-id="18385-187">Set the Optional Header Value option too"basic."</span></span>

<span data-ttu-id="18385-188">WWW-Authenticate 헤더는 401 응답 코드에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-188">The WWW-Authenticate header is only applicable for 401 response codes.</span></span>

### <a name="token-auth-ignore-url-case"></a><span data-ttu-id="18385-189">토큰 인증 URL 대/소문자 무시</span><span class="sxs-lookup"><span data-stu-id="18385-189">Token Auth Ignore URL Case</span></span>
<span data-ttu-id="18385-190">**목적:** 토큰 기반 인증으로 수행되는 URL 비교에서 대/소문자를 구분하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-190">**Purpose:** Determines whether URL comparisons made by Token-Based Authentication will be case-sensitive.</span></span>

<span data-ttu-id="18385-191">이 기능에 의해 영향을 받는 hello 매개 변수는.</span><span class="sxs-lookup"><span data-stu-id="18385-191">hello parameters affected by this feature are:</span></span>

- <span data-ttu-id="18385-192">ec_url_allow</span><span class="sxs-lookup"><span data-stu-id="18385-192">ec_url_allow</span></span>
- <span data-ttu-id="18385-193">ec_ref_allow</span><span class="sxs-lookup"><span data-stu-id="18385-193">ec_ref_allow</span></span>
- <span data-ttu-id="18385-194">ec_ref_deny</span><span class="sxs-lookup"><span data-stu-id="18385-194">ec_ref_deny</span></span>

<span data-ttu-id="18385-195">유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-195">Valid values are:</span></span>

<span data-ttu-id="18385-196">값</span><span class="sxs-lookup"><span data-stu-id="18385-196">Value</span></span>|<span data-ttu-id="18385-197">결과</span><span class="sxs-lookup"><span data-stu-id="18385-197">Result</span></span>
---|----
<span data-ttu-id="18385-198">사용</span><span class="sxs-lookup"><span data-stu-id="18385-198">Enabled</span></span>|<span data-ttu-id="18385-199">토큰 기반 인증 매개 변수에 대 한 Url을 비교할 때이 지 서버 tooignore 대/소문자를 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-199">Causes our edge server tooignore case when comparing URLs for Token-Based Authentication parameters.</span></span>
<span data-ttu-id="18385-200">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-200">Disabled</span></span>|<span data-ttu-id="18385-201">Hello 기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-201">Restores hello default behavior.</span></span> <span data-ttu-id="18385-202">토큰 인증 toobe 대/소문자 구분에 대 한 URL 비교 hello 기본 동작이입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-202">hello default behavior is for URL comparisons for Token Authentication toobe case-sensitive.</span></span>

<span data-ttu-id="18385-203">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-203">**Default Behavior:** Disabled.</span></span>
 
### <a name="token-auth-parameter"></a><span data-ttu-id="18385-204">토큰 인증 매개 변수</span><span class="sxs-lookup"><span data-stu-id="18385-204">Token Auth Parameter</span></span>
<span data-ttu-id="18385-205">**목적:** hello 토큰 기반 인증 쿼리 문자열 매개 변수 이름을 바꿔야 하는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-205">**Purpose:** Determines whether hello Token-Based Authentication query string parameter should be renamed.</span></span>

<span data-ttu-id="18385-206">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-206">Key information:</span></span>

- <span data-ttu-id="18385-207">값 옵션 정의 hello 쿼리 문자열 매개 변수 이름을 통해 토큰을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-207">The Value option defines hello query string parameter name through which a token may be specified.</span></span>
- <span data-ttu-id="18385-208">값 옵션을 너무 설정할 수 없습니다. "ec_token."</span><span class="sxs-lookup"><span data-stu-id="18385-208">The Value option cannot be set too"ec_token."</span></span>
- <span data-ttu-id="18385-209">값 옵션만에 정의 된 해당 hello 이름이 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="18385-209">Make sure that hello name defined in the Value option only</span></span> 
- <span data-ttu-id="18385-210">유효한 URL 문자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-210">contains valid URL characters.</span></span>

<span data-ttu-id="18385-211">값</span><span class="sxs-lookup"><span data-stu-id="18385-211">Value</span></span>|<span data-ttu-id="18385-212">결과</span><span class="sxs-lookup"><span data-stu-id="18385-212">Result</span></span>
----|----
<span data-ttu-id="18385-213">사용</span><span class="sxs-lookup"><span data-stu-id="18385-213">Enabled</span></span>|<span data-ttu-id="18385-214">값 옵션이 있는 토큰을 정의 해야 하는 hello 쿼리 문자열 매개 변수 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-214">The Value option defines hello query string parameter name through which tokens should be defined.</span></span>
<span data-ttu-id="18385-215">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-215">Disabled</span></span>|<span data-ttu-id="18385-216">토큰은 hello 요청 URL에는 정의 되지 않은 쿼리 문자열 매개 변수로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-216">A token may be specified as an undefined query string parameter in hello request URL.</span></span>

<span data-ttu-id="18385-217">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-217">**Default Behavior:** Disabled.</span></span> <span data-ttu-id="18385-218">토큰은 hello 요청 URL에는 정의 되지 않은 쿼리 문자열 매개 변수로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-218">A token may be specified as an undefined query string parameter in hello request URL.</span></span>

## <a name="caching"></a><span data-ttu-id="18385-219">구성</span><span class="sxs-lookup"><span data-stu-id="18385-219">Caching</span></span>

<span data-ttu-id="18385-220">이러한 기능은 디자인 된 toocustomize 시기와 방법을 콘텐츠가 캐시 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-220">These features are designed toocustomize when and how content is cached.</span></span>

<span data-ttu-id="18385-221">이름</span><span class="sxs-lookup"><span data-stu-id="18385-221">Name</span></span> | <span data-ttu-id="18385-222">목적</span><span class="sxs-lookup"><span data-stu-id="18385-222">Purpose</span></span>
-----|--------
<span data-ttu-id="18385-223">대역폭 매개 변수</span><span class="sxs-lookup"><span data-stu-id="18385-223">Bandwidth Parameters</span></span> | <span data-ttu-id="18385-224">대역폭 제한 매개 변수(예: ec_rate 및 ec_prebuf)를 활성화할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-224">Determines whether bandwidth throttling parameters (i.e., ec_rate and ec_prebuf) will be active.</span></span>
<span data-ttu-id="18385-225">대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="18385-225">Bandwidth Throttling</span></span> | <span data-ttu-id="18385-226">이 지 서버에서 제공 하는 hello 응답에 대 한 hello 대역폭을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-226">Throttles hello bandwidth for hello response provided by our edge servers.</span></span>
<span data-ttu-id="18385-227">바이패스 캐시</span><span class="sxs-lookup"><span data-stu-id="18385-227">Bypass Cache</span></span> | <span data-ttu-id="18385-228">Hello 요청 우리의 캐싱 기술을 활용할 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-228">Determines whether hello request can leverage our caching technology.</span></span>
<span data-ttu-id="18385-229">Cache-Control 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="18385-229">Cache-Control Header Treatment</span></span> | <span data-ttu-id="18385-230">컨트롤은 hello에 지 서버에서 캐시 제어 헤더의 생성을 hello 외부 Max-age 기능을 활성화 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="18385-230">Controls hello generation of Cache-Control headers by hello edge server when External Max-Age feature is active.</span></span>
<span data-ttu-id="18385-231">Cache-Key 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="18385-231">Cache-Key Query String</span></span> | <span data-ttu-id="18385-232">Hello 캐시 키 요청과 연결 된 쿼리 문자열 매개 변수를 제외 포함 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-232">Determines whether hello cache-key will include or exclude query string parameters associated with a request.</span></span>
<span data-ttu-id="18385-233">Cache-Key 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-233">Cache-Key Rewrite</span></span> | <span data-ttu-id="18385-234">요청과 연결 된 hello 캐시 키를 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-234">Rewrites hello cache-key associated with a request.</span></span>
<span data-ttu-id="18385-235">전체 캐시 채우기</span><span class="sxs-lookup"><span data-stu-id="18385-235">Complete Cache Fill</span></span> | <span data-ttu-id="18385-236">요청 결과, 에지 서버에서 캐시가 부분적으로 누락된 경우 수행할 작업을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-236">Determines what happens when a request results in a partial cache miss on an edge server.</span></span>
<span data-ttu-id="18385-237">압축 파일 형식</span><span class="sxs-lookup"><span data-stu-id="18385-237">Compress File Types</span></span> | <span data-ttu-id="18385-238">Hello 서버에서 압축 되도록 하는 hello 파일 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-238">Defines hello file formats that will be compressed on hello server.</span></span>
<span data-ttu-id="18385-239">기본 내부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="18385-239">Default Internal Max-Age</span></span> | <span data-ttu-id="18385-240">Edge 서버 tooorigin 서버 캐시 유효성 재검사 hello 기본 최대 처리 기간 간격을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-240">Determines hello default max-age interval for edge server tooorigin server cache revalidation.</span></span>
<span data-ttu-id="18385-241">만료 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="18385-241">Expires Header Treatment</span></span> | <span data-ttu-id="18385-242">컨트롤에 지 서버에서 Expires 헤더의 생성을 hello hello 외부 Max-age 기능을 활성화 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="18385-242">Controls hello generation of Expires headers by an edge server when hello External Max-Age feature is active.</span></span>
<span data-ttu-id="18385-243">외부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="18385-243">External Max-Age</span></span> | <span data-ttu-id="18385-244">브라우저 tooedge 서버 캐시 유효성 재검사 hello 최대 처리 기간 간격을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-244">Determines hello max-age interval for browser tooedge server cache revalidation.</span></span>
<span data-ttu-id="18385-245">강제 내부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="18385-245">Force Internal Max-Age</span></span> | <span data-ttu-id="18385-246">Edge 서버 tooorigin 서버 캐시 유효성 재검사 hello 최대 처리 기간 간격을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-246">Determines hello max-age interval for edge server tooorigin server cache revalidation.</span></span>
<span data-ttu-id="18385-247">H.264 지원(HTTP 점진적 다운로드)</span><span class="sxs-lookup"><span data-stu-id="18385-247">H.264 Support (HTTP Progressive Download)</span></span> | <span data-ttu-id="18385-248">H.264 hello 유형의 파일 형식을 사용 하는 toostream 수 있는 콘텐츠를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-248">Determines hello types of H.264 file formats that may be used toostream content.</span></span>
<span data-ttu-id="18385-249">No-Cache 요청 부여</span><span class="sxs-lookup"><span data-stu-id="18385-249">Honor No-Cache Request</span></span> | <span data-ttu-id="18385-250">여부 HTTP 클라이언트의 캐시 없음 요청 전달 toohello 원본 서버를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-250">Determines whether an HTTP client's no-cache requests will be forwarded toohello origin server.</span></span>
<span data-ttu-id="18385-251">원본 No-Cache 무시</span><span class="sxs-lookup"><span data-stu-id="18385-251">Ignore Origin No-Cache</span></span> | <span data-ttu-id="18385-252">CDN이 원본 서버에서 제공되는 특정 지시문을 무시할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-252">Determines whether our CDN will ignore certain directives served from an origin server.</span></span>
<span data-ttu-id="18385-253">적절하지 않은 범위 무시</span><span class="sxs-lookup"><span data-stu-id="18385-253">Ignore Unsatisfiable Ranges</span></span> | <span data-ttu-id="18385-254">반환 되는 tooclients 요청 416 요청한 범위가 충분 하지 않음 상태 코드를 생성할 때 hello 응답을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-254">Determines hello response that will be returned tooclients when a request generates a 416 Requested Range Not Satisfiable status code.</span></span>
<span data-ttu-id="18385-255">내부 Max-Stale</span><span class="sxs-lookup"><span data-stu-id="18385-255">Internal Max-Stale</span></span> | <span data-ttu-id="18385-256">캐시 된 자산을 구현 될 수 있습니다 hello 정상적으로 종료 시간 이전 시간에 지 서버에서 hello에 지 서버 경우 없습니다 toorevalidate hello hello 원본 서버와 캐시 된 자산을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-256">Controls how long past hello normal expiration time a cached asset may be served from an edge server when hello edge server is unable toorevalidate hello cached asset with hello origin server.</span></span>
<span data-ttu-id="18385-257">부분 캐시 공유</span><span class="sxs-lookup"><span data-stu-id="18385-257">Partial Cache Sharing</span></span> | <span data-ttu-id="18385-258">요청에서 부분적으로 캐시된 콘텐츠를 생성할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-258">Determines whether a request can generate partially cached content.</span></span>
<span data-ttu-id="18385-259">캐시된 콘텐츠 사전 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="18385-259">Prevalidate Cached Content</span></span> | <span data-ttu-id="18385-260">TTL이 만료되기 전에 캐시된 콘텐츠로 미리 유효성 재검사할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-260">Determines whether cached content will be eligible for early revalidation before its TTL expires.</span></span>
<span data-ttu-id="18385-261">0바이트 캐시 파일 새로 고침</span><span class="sxs-lookup"><span data-stu-id="18385-261">Refresh Zero-Byte Cache Files</span></span> | <span data-ttu-id="18385-262">0바이트 캐시 자산에 대한 HTTP 클라이언트 요청이 에지 서버에 의해 처리되는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-262">Determines how an HTTP client's request for a 0-byte cache asset is handled by our edge servers.</span></span>
<span data-ttu-id="18385-263">캐시 가능한 상태 코드 집합</span><span class="sxs-lookup"><span data-stu-id="18385-263">Set Cacheable Status Codes</span></span> | <span data-ttu-id="18385-264">캐시 된 콘텐츠 발생할 수 있는 상태 코드 hello 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-264">Defines hello set of status codes that can result in cached content.</span></span>
<span data-ttu-id="18385-265">오류 시 오래된 콘텐츠 배달</span><span class="sxs-lookup"><span data-stu-id="18385-265">Stale Content Delivery on Error</span></span> | <span data-ttu-id="18385-266">캐시 유효성 재검사 중 또는 검색 하는 동안 hello hello 고객 원본 서버에서 콘텐츠를 요청 하면 오류가 발생할 때 배달 될 캐시 된 콘텐츠 만료 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-266">Determines whether expired cached content will be delivered when an error occurs during cache revalidation or when retrieving hello requested content from hello customer origin server.</span></span>
<span data-ttu-id="18385-267">유효성 재검사 중 기한 경과</span><span class="sxs-lookup"><span data-stu-id="18385-267">Stale While Revalidate</span></span> | <span data-ttu-id="18385-268">유효성을 다시 수행 하는 동안이 지 서버 tooserve 오래 된 클라이언트 toohello 요청자를 허용 하 여 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-268">Improves performance by allowing our edge servers tooserve stale client toohello requester while revalidation takes place.</span></span>
<span data-ttu-id="18385-269">주석</span><span class="sxs-lookup"><span data-stu-id="18385-269">Comment</span></span> | <span data-ttu-id="18385-270">hello 주석 기능을 사용 하는 참고 toobe 규칙 내에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-270">hello Comment feature allows a note toobe added within a rule.</span></span>

###<a name="bandwidth-parameters"></a><span data-ttu-id="18385-271">대역폭 매개 변수</span><span class="sxs-lookup"><span data-stu-id="18385-271">Bandwidth Parameters</span></span>
<span data-ttu-id="18385-272">**목적:** 대역폭 제한 매개 변수(예: ec_rate 및 ec_prebuf)를 활성화하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-272">**Purpose:** Determines whether bandwidth throttling parameters (i.e., ec_rate and ec_prebuf) will be active.</span></span>

<span data-ttu-id="18385-273">대역폭 조정 매개 변수는 클라이언트의 요청에 대 한 hello 데이터 전송 속도 제한 tooa 사용자 지정 비율 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-273">Bandwidth throttling parameters determine whether hello data transfer rate for a client's request will be limited tooa custom rate.</span></span>

<span data-ttu-id="18385-274">값</span><span class="sxs-lookup"><span data-stu-id="18385-274">Value</span></span>|<span data-ttu-id="18385-275">결과</span><span class="sxs-lookup"><span data-stu-id="18385-275">Result</span></span>
--|--
<span data-ttu-id="18385-276">사용</span><span class="sxs-lookup"><span data-stu-id="18385-276">Enabled</span></span>|<span data-ttu-id="18385-277">Edge 서버 toohonor 대역폭을으로 요청을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-277">Allows our edge servers toohonor bandwidth throttling requests.</span></span>
<span data-ttu-id="18385-278">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-278">Disabled</span></span>|<span data-ttu-id="18385-279">Edge 서버 tooignore 대역폭 매개 변수를 제한 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-279">Causes our edge servers tooignore bandwidth throttling parameters.</span></span> <span data-ttu-id="18385-280">hello 요청 (즉, 대역폭 제한) 없이 콘텐츠를 정상적으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-280">hello requested content will be served normally (i.e., without bandwidth throttling).</span></span>

<span data-ttu-id="18385-281">**기본 동작**: 사용</span><span class="sxs-lookup"><span data-stu-id="18385-281">**Default Behavior:** Enabled.</span></span>

###<a name="bandwidth-throttling"></a><span data-ttu-id="18385-282">대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="18385-282">Bandwidth Throttling</span></span>
<span data-ttu-id="18385-283">**목적:** 스로틀 hello 우리의 지 서버에서 제공 하는 hello 응답에 대 한 대역폭입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-283">**Purpose:** Throttles hello bandwidth for hello response provided by our edge servers.</span></span>

<span data-ttu-id="18385-284">Hello 다음 옵션을 모두 정의 tooproperly 대역폭 제한 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-284">Both of hello following options must be defined tooproperly set up bandwidth throttling.</span></span>

<span data-ttu-id="18385-285">옵션</span><span class="sxs-lookup"><span data-stu-id="18385-285">Option</span></span>|<span data-ttu-id="18385-286">설명</span><span class="sxs-lookup"><span data-stu-id="18385-286">Description</span></span>
--|--
<span data-ttu-id="18385-287">초당 킬로바이트</span><span class="sxs-lookup"><span data-stu-id="18385-287">Kbytes per second</span></span>|<span data-ttu-id="18385-288">이 옵션 toohello 최대 대역폭 (k b / 초)을 사용 하는 toodeliver hello 응답 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-288">Set this option toohello maximum bandwidth (Kb per second) that may be used toodeliver hello response.</span></span>
<span data-ttu-id="18385-289">Prebuf 초</span><span class="sxs-lookup"><span data-stu-id="18385-289">Prebuf seconds</span></span>|<span data-ttu-id="18385-290">이 옵션 toohello 번호는에 지 서버에서 제한 대역폭 될 때까지 대기 하는 시간 (초)을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-290">Set this option toohello number of seconds that our edge servers will wait until throttling bandwidth.</span></span> <span data-ttu-id="18385-291">hello의이 시간 동안 무제한 대역폭의 목적은 tooprevent 미디어 플레이어에서 일지 또는 버퍼링 toobandwidth 제한 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-291">hello purpose of this time period of unrestricted bandwidth is tooprevent a media player from experiencing stuttering or buffering issues due toobandwidth throttling.</span></span>

<span data-ttu-id="18385-292">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-292">**Default Behavior:** Disabled.</span></span>

###<a name="bypass-cache"></a><span data-ttu-id="18385-293">바이패스 캐시</span><span class="sxs-lookup"><span data-stu-id="18385-293">Bypass Cache</span></span>
<span data-ttu-id="18385-294">**목적:** hello 요청 우리의 캐싱 기술을 활용할 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-294">**Purpose:** Determines whether hello request can leverage our caching technology.</span></span>

<span data-ttu-id="18385-295">값</span><span class="sxs-lookup"><span data-stu-id="18385-295">Value</span></span>|<span data-ttu-id="18385-296">결과</span><span class="sxs-lookup"><span data-stu-id="18385-296">Result</span></span>
--|--
<span data-ttu-id="18385-297">사용</span><span class="sxs-lookup"><span data-stu-id="18385-297">Enabled</span></span>|<span data-ttu-id="18385-298">Hello 콘텐츠는에 지 서버에서 이전에 캐시 된 경우에 toohello 원본 서버를 통해 모든 요청 toofall을 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-298">Causes all requests toofall through toohello origin server, even if hello content was previously cached on edge servers.</span></span>
<span data-ttu-id="18385-299">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-299">Disabled</span></span>|<span data-ttu-id="18385-300">응답 헤더에 정의 된 toohello 캐시 정책에 따라 toocache 자산에 지 서버에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-300">Causes edge servers toocache assets according toohello cache policy defined in its response headers.</span></span>

<span data-ttu-id="18385-301">**기본 동작:**</span><span class="sxs-lookup"><span data-stu-id="18385-301">**Default Behavior:**</span></span>

- <span data-ttu-id="18385-302">**HTTP Large:** 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-302">**HTTP Large:** Disabled</span></span>

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a><span data-ttu-id="18385-303">Cache-Control 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="18385-303">Cache Control Header Treatment</span></span>
<span data-ttu-id="18385-304">**목적:** 외부 Max-age 기능을 활성화 하는 경우 hello에 지 서버에서 캐시 제어 헤더의 hello 생성을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-304">**Purpose:** Controls hello generation of Cache-Control headers by hello edge server when External Max-Age Feature is active.</span></span>

<span data-ttu-id="18385-305">이 구성 유형은 tooplace hello 외부 Max-age 및 hello 캐시 컨트롤 헤더 처리 기능에는 가장 쉬운 방법은 tooachieve hello 동일한 문에서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-305">hello easiest way tooachieve this type of configuration is tooplace hello External Max-Age and hello Cache-Control Header Treatment features in hello same statement.</span></span>

<span data-ttu-id="18385-306">값</span><span class="sxs-lookup"><span data-stu-id="18385-306">Value</span></span>|<span data-ttu-id="18385-307">결과</span><span class="sxs-lookup"><span data-stu-id="18385-307">Result</span></span>
--|--
<span data-ttu-id="18385-308">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-308">Overwrite</span></span>|<span data-ttu-id="18385-309">해당 hello 다음 작업 수행을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-309">Ensures that hello following actions will take place:</span></span><br/> <span data-ttu-id="18385-310">-Hello 원본 서버에 의해 생성 된 Cache-control 헤더를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="18385-310">- Overwrites the Cache-Control header generated by hello origin server.</span></span> <br/><span data-ttu-id="18385-311">-Hello 외부 Max-age 기능 toohello 응답에서 생성 된 Cache-control 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-311">- Adds the Cache-Control header produced by hello External Max-Age feature toohello response.</span></span>
<span data-ttu-id="18385-312">통과</span><span class="sxs-lookup"><span data-stu-id="18385-312">Pass Through</span></span>|<span data-ttu-id="18385-313">Hello 외부 Max-age 기능에 의해 생성 된 Cache-control 헤더 toohello 응답 하지 않습니다 추가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-313">Ensures that the Cache-Control header produced by hello External Max-Age feature is never added toohello response.</span></span> <br/> <span data-ttu-id="18385-314">Hello 원본 서버에서 생성 하는 Cache-control 헤더 toohello 최종 사용자를 통해 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-314">If hello origin server produces a Cache-Control header, it will pass through toohello end-user.</span></span> <br/> <span data-ttu-id="18385-315">Hello 원본 서버는 캐시 제어 헤더 다음이 옵션을 생성 하지 포함 될 수 있습니다 원인 hello 응답 헤더 toonot 캐시 컨트롤 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-315">If hello origin server does not produce a Cache-Control header, then this option may cause hello response header toonot contain a Cache-Control header.</span></span>
<span data-ttu-id="18385-316">없는 경우 추가</span><span class="sxs-lookup"><span data-stu-id="18385-316">Add if Missing</span></span>|<span data-ttu-id="18385-317">캐시 컨트롤 헤더 hello 원본 서버에서 수신 되지 않았습니다,이 옵션 hello 외부 Max-age 기능에 의해 생성 된 Cache-control 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-317">If a Cache-Control header was not received from hello origin server, then this option adds the Cache-Control header produced by hello External Max-Age feature.</span></span> <span data-ttu-id="18385-318">이 옵션은 모든 자산에 Cache-Control 헤더를 할당하도록 하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-318">This option is useful for ensuring that all assets will be assigned a Cache-Control header.</span></span>
<span data-ttu-id="18385-319">제거</span><span class="sxs-lookup"><span data-stu-id="18385-319">Remove</span></span>| <span data-ttu-id="18385-320">이 옵션을 사용 하면 캐시 컨트롤 헤더 hello 헤더 응답과 함께 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-320">This option ensures that a Cache-Control header is not included with hello header response.</span></span> <span data-ttu-id="18385-321">캐시 컨트롤 헤더에 이미 할당 된 경우 다음 것에서 제거 됩니다 hello 헤더 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-321">If a Cache-Control header has already been assigned, then it will be stripped from hello header response.</span></span>

<span data-ttu-id="18385-322">**기본 동작:** 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-322">**Default Behavior:** Overwrite.</span></span>

###<a name="cache-key-query-string"></a><span data-ttu-id="18385-323">Cache-Key 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="18385-323">Cache-Key Query String</span></span>
<span data-ttu-id="18385-324">**목적:** cache-key에서 요청과 관련된 쿼리 문자열 매개 변수를 포함할지 또는 제외할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-324">**Purpose:** Determines whether the cache-key will include or exclude query string parameters associated with a request.</span></span>

<span data-ttu-id="18385-325">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-325">Key information:</span></span>

- <span data-ttu-id="18385-326">쿼리 문자열 매개 변수 이름을 둘 이상 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-326">Specify one or more query string parameter name(s).</span></span> <span data-ttu-id="18385-327">각 매개 변수 이름은 단일 공백으로 구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-327">Each parameter name should be delimited with a single space.</span></span>
- <span data-ttu-id="18385-328">이 기능은 쿼리 문자열 매개 변수를 포함 하거나 hello 캐시 키에서 제외 됩니다 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-328">This feature determines whether query string parameters will be included or excluded from hello cache-key.</span></span> <span data-ttu-id="18385-329">각 옵션에 제공되는 추가 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-329">Additional information is provided for each option below.</span></span>

<span data-ttu-id="18385-330">형식</span><span class="sxs-lookup"><span data-stu-id="18385-330">Type</span></span>|<span data-ttu-id="18385-331">설명</span><span class="sxs-lookup"><span data-stu-id="18385-331">Description</span></span>
--|--
 <span data-ttu-id="18385-332">포함</span><span class="sxs-lookup"><span data-stu-id="18385-332">Include</span></span>|  <span data-ttu-id="18385-333">지정 된 각 매개 변수에 해야 hello 캐시 키에 포함 되어야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18385-333">Indicates that each specified parameter should be included in hello cache-key.</span></span> <span data-ttu-id="18385-334">이 기능에 정의된 쿼리 문자열 매개 변수의 고유한 값을 포함하는 요청마다 고유한 cache-key가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-334">A unique cache-key will be generated for each request that contains a unique value for a query string parameter defined in this feature.</span></span> 
 <span data-ttu-id="18385-335">모두 포함</span><span class="sxs-lookup"><span data-stu-id="18385-335">Include All</span></span>  |<span data-ttu-id="18385-336">고유한 쿼리 문자열이 포함 된 각 요청 tooan 자산에 대 한 고유 캐시 키 만들어질 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18385-336">Indicates that a unique cache-key will be created for each request tooan asset that includes a unique query string.</span></span> <span data-ttu-id="18385-337">이러한 유형의 구성 하므로 캐시 적중 횟수의 작은 비율을 tooa 않을 일반적으로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-337">This type of configuration is not typically recommended since it may lead tooa small percentage of cache hits.</span></span> <span data-ttu-id="18385-338">이렇게 하면 미치게 될 tooserve 더 많은 요청이 이후 hello 원본 서버의 hello 로드가 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="18385-338">This will increase hello load on hello origin server, since it will have tooserve more requests.</span></span> <span data-ttu-id="18385-339">이 구성은 hello 캐싱 "고유-cache" 쿼리 문자열 캐싱 페이지 라고 하는 동작을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-339">This configuration duplicates hello caching behavior known as "unique-cache" on the Query-String Caching page.</span></span> 
 <span data-ttu-id="18385-340">제외</span><span class="sxs-lookup"><span data-stu-id="18385-340">Exclude</span></span> | <span data-ttu-id="18385-341">해당만 hello 지정 매개 변수는 hello 캐시 키에서 제외 됩니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18385-341">Indicates that only hello specified parameter(s) will be excluded from hello cache-key.</span></span> <span data-ttu-id="18385-342">다른 모든 쿼리 문자열 매개 변수는 hello 캐시 키에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-342">All other query string parameters will be included in hello cache-key.</span></span> 
 <span data-ttu-id="18385-343">모두 제외</span><span class="sxs-lookup"><span data-stu-id="18385-343">Exclude All</span></span>  |<span data-ttu-id="18385-344">모든 쿼리 문자열 매개 변수가 됩니다 hello 캐시 키에서 제외 되어야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18385-344">Indicates that all query string parameters will be excluded from hello cache-key.</span></span> <span data-ttu-id="18385-345">이 구성은 hello 기본 캐싱 쿼리 문자열 캐싱 페이지에 "표준 캐시"으로 알려진 동작을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-345">This configuration duplicates hello default caching behavior, which is known as "standard-cache" on the Query-String Caching page.</span></span> 

<span data-ttu-id="18385-346">HTTP 규칙 엔진의 hello 전원 toocustomize hello 방식 으로를 쿼리 문자열 캐싱을 구현 되는에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-346">hello power of HTTP Rules Engine allows you toocustomize hello manner in which query string caching is implemented.</span></span> <span data-ttu-id="18385-347">예를 들어 특정 위치 또는 파일 형식에서만 쿼리 문자열 캐싱을 수행하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-347">For example, you can specify that query string caching only be performed on certain locations or file types.</span></span>

<span data-ttu-id="18385-348">Tooduplicate hello 쿼리 문자열 캐싱 동작으로 "no cache" 쿼리 문자열 캐싱 페이지, 원하는 경우 해야 합니다 toocreate는 URL 쿼리 와일드 카드 일치 조건과 바이패스 캐시 기능을 포함 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-348">If you would like tooduplicate hello query string caching behavior known as "no-cache" on the Query-String Caching page, then you will need toocreate a rule that contains a URL Query Wildcard match condition and a Bypass Cache feature.</span></span> <span data-ttu-id="18385-349">URL 쿼리 와일드 카드 일치 조건을 hello tooan 별표 (*)을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-349">hello URL Query Wildcard match condition should be set tooan asterisk (*).</span></span>

#### <a name="sample-scenarios"></a><span data-ttu-id="18385-350">샘플 시나리오</span><span class="sxs-lookup"><span data-stu-id="18385-350">Sample Scenarios</span></span>

<span data-ttu-id="18385-351">이 기능의 샘플 사용법이 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-351">Sample usage for this feature is provided below.</span></span> <span data-ttu-id="18385-352">예제 요청 및 hello에 대 한 기본 캐시 키 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-352">A sample request and hello default cache-key are provided below.</span></span>

- <span data-ttu-id="18385-353">**샘플 요청:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01</span><span class="sxs-lookup"><span data-stu-id="18385-353">**Sample request:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01</span></span>
- <span data-ttu-id="18385-354">**기본 cache-key:** /800001/Origin/folder/asset.htm</span><span class="sxs-lookup"><span data-stu-id="18385-354">**Default cache-key:** /800001/Origin/folder/asset.htm</span></span>

##### <a name="include"></a><span data-ttu-id="18385-355">포함</span><span class="sxs-lookup"><span data-stu-id="18385-355">Include</span></span>

<span data-ttu-id="18385-356">샘플 구성:</span><span class="sxs-lookup"><span data-stu-id="18385-356">Sample configuration:</span></span>

- <span data-ttu-id="18385-357">**형식:** 포함</span><span class="sxs-lookup"><span data-stu-id="18385-357">**Type:** Include</span></span>
- <span data-ttu-id="18385-358">**매개 변수:** language</span><span class="sxs-lookup"><span data-stu-id="18385-358">**Parameter(s):** language</span></span>

<span data-ttu-id="18385-359">이러한 유형의 구성 hello 다음 쿼리 문자열 매개 변수 캐시 키 생성:</span><span class="sxs-lookup"><span data-stu-id="18385-359">This type of configuration would generate hello following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a><span data-ttu-id="18385-360">모두 포함</span><span class="sxs-lookup"><span data-stu-id="18385-360">Include All</span></span>

<span data-ttu-id="18385-361">샘플 구성:</span><span class="sxs-lookup"><span data-stu-id="18385-361">Sample configuration:</span></span>

- <span data-ttu-id="18385-362">**형식:** 모두 포함</span><span class="sxs-lookup"><span data-stu-id="18385-362">**Type:** Include All</span></span>

<span data-ttu-id="18385-363">이러한 유형의 구성 hello 다음 쿼리 문자열 매개 변수 캐시 키 생성:</span><span class="sxs-lookup"><span data-stu-id="18385-363">This type of configuration would generate hello following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a><span data-ttu-id="18385-364">제외</span><span class="sxs-lookup"><span data-stu-id="18385-364">Exclude</span></span>

<span data-ttu-id="18385-365">샘플 구성:</span><span class="sxs-lookup"><span data-stu-id="18385-365">Sample configuration:</span></span>

- <span data-ttu-id="18385-366">**형식:** 제외</span><span class="sxs-lookup"><span data-stu-id="18385-366">**Type:** Exclude</span></span>
- <span data-ttu-id="18385-367">**매개 변수:** sessionid userid</span><span class="sxs-lookup"><span data-stu-id="18385-367">**Parameter(s):** sessionid userid</span></span>

<span data-ttu-id="18385-368">이러한 유형의 구성 hello 다음 쿼리 문자열 매개 변수 캐시 키 생성:</span><span class="sxs-lookup"><span data-stu-id="18385-368">This type of configuration would generate hello following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a><span data-ttu-id="18385-369">모두 제외</span><span class="sxs-lookup"><span data-stu-id="18385-369">Exclude All</span></span>

<span data-ttu-id="18385-370">샘플 구성:</span><span class="sxs-lookup"><span data-stu-id="18385-370">Sample configuration:</span></span>

- <span data-ttu-id="18385-371">**형식:** 모두 제외</span><span class="sxs-lookup"><span data-stu-id="18385-371">**Type:** Exclude All</span></span>

<span data-ttu-id="18385-372">이러한 유형의 구성 hello 다음 쿼리 문자열 매개 변수 캐시 키 생성:</span><span class="sxs-lookup"><span data-stu-id="18385-372">This type of configuration would generate hello following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a><span data-ttu-id="18385-373">Cache-Key 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-373">Cache-Key Rewrite</span></span>
<span data-ttu-id="18385-374">**목적:** 캡슐화 hello 요청과 연결 된 캐시 키입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-374">**Purpose:** Rewrites hello cache-key associated with a request.</span></span>

<span data-ttu-id="18385-375">캐시 키가 캐시의 hello 목적을 위해 자산을 식별 하는 hello 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-375">A cache-key is hello relative path that identifies an asset for hello purposes of caching.</span></span> <span data-ttu-id="18385-376">즉, 서버는 캐시 된 버전의 캐시 키에 정의 된 대로 tooits 경로 따라 자산을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-376">In other words, our servers will check for a cached version of an asset according tooits path as defined by its cache-key.</span></span>

<span data-ttu-id="18385-377">모두 hello 다음 옵션을 정의 하 여이 기능을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-377">Configure this feature by defining both of hello following options:</span></span>

<span data-ttu-id="18385-378">옵션</span><span class="sxs-lookup"><span data-stu-id="18385-378">Option</span></span>|<span data-ttu-id="18385-379">설명</span><span class="sxs-lookup"><span data-stu-id="18385-379">Description</span></span>
--|--
<span data-ttu-id="18385-380">원래 경로</span><span class="sxs-lookup"><span data-stu-id="18385-380">Original Path</span></span>| <span data-ttu-id="18385-381">캐시 키를 다시 작성 됩니다 요청의 hello 상대 경로 toohello 유형을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-381">Define hello relative path toohello types of requests whose cache-key will be rewritten.</span></span> <span data-ttu-id="18385-382">상대 경로는 기본 경로를 선택한 다음 정규식 패턴을 정의함으로써 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-382">A relative path can be defined by selecting a base origin path and then defining a regular expression pattern.</span></span>
<span data-ttu-id="18385-383">새 경로</span><span class="sxs-lookup"><span data-stu-id="18385-383">New Path</span></span>|<span data-ttu-id="18385-384">Hello hello 새 캐시 키에 대 한 상대 경로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-384">Define hello relative path for hello new cache-key.</span></span> <span data-ttu-id="18385-385">상대 경로는 기본 경로를 선택한 다음 정규식 패턴을 정의함으로써 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-385">A relative path can be defined by selecting a base origin path and then defining a regular expression pattern.</span></span> <span data-ttu-id="18385-386">HTTP 변수의 hello 사용을 통해이 상대 경로 동적으로 생성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-386">This relative path can be dynamically constructed through hello use of HTTP variables</span></span>
<span data-ttu-id="18385-387">**기본 동작:** 요청의 캐시 키 hello 요청 URI에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-387">**Default Behavior:** A request's cache-key is determined by hello request URI.</span></span>

###<a name="complete-cache-fill"></a><span data-ttu-id="18385-388">전체 캐시 채우기</span><span class="sxs-lookup"><span data-stu-id="18385-388">Complete Cache Fill</span></span>
<span data-ttu-id="18385-389">**목적:** 요청으로 인해 에지 서버에서 부분 캐시가 누락된 경우 수행할 작업을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-389">**Purpose:** Determines what happens when a request results in a partial cache miss on an edge server.</span></span>

<span data-ttu-id="18385-390">부분 캐시 누락 tooan 완전히 다운로드 된에 지 서버 없었던 자산에 대 한 hello 캐시 상태를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-390">A partial cache miss describes hello cache status for an asset that was not completely downloaded tooan edge server.</span></span> <span data-ttu-id="18385-391">자산 부분적 으로만에 지 서버에 캐시 되는, 다음 hello 해당 자산에 대 한 다음 요청이 전달 됩니다 다시 toohello 원본 서버.</span><span class="sxs-lookup"><span data-stu-id="18385-391">If an asset is only partially cached on an edge server, then hello next request for that asset will be forwarded again toohello origin server.</span></span>
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
<span data-ttu-id="18385-392">부분 캐시 누락은 일반적으로 사용자가 다운로드를 중단한 후에 발생하거나 HTTP 범위 요청을 사용하여 단독으로 요청된 자산에 대해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-392">A partial cache miss typically occurs after a user aborts a download or for assets that are solely requested using HTTP range requests.</span></span> <span data-ttu-id="18385-393">이 기능은 큰 자산에 대 한 가장 유용한 여기서 사용자가 다운로드 되지 것입니다 일반적으로 이러한 시작 toofinish (예: 비디오) 에서입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-393">This feature is most useful for large assets where users will not typically download them from start toofinish (e.g., videos).</span></span> <span data-ttu-id="18385-394">결과적으로,이 기능은 hello HTTP 많은 플랫폼에서 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-394">As a result, this feature is enabled by default on hello HTTP Large platform.</span></span> <span data-ttu-id="18385-395">다른 모든 플랫폼에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-395">It is disabled on all other platforms.</span></span>

<span data-ttu-id="18385-396">Hello 부하 고객 원본 서버를 줄여야 하 고는 고객에 게 콘텐츠를 다운로드 하는 hello 속도 높일 이후 tooleave hello 기본 구성은 hello HTTP 큰 플랫폼에 대 한이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-396">It is recommended tooleave hello default configuration for hello HTTP Large platform, since it will reduce hello load on your customer origin server and increase hello speed at which your customers download your content.</span></span>

<span data-ttu-id="18385-397">설정을 추적 되는 캐시에 toohello 방식으로 인해이 기능을 연결할 수 일치 조건을 다음 hello로: 가장자리 Cname, 리터럴 헤더를 요청, 요청 헤더 와일드 카드, URL 쿼리 리터럴 및 쿼리 와일드 카드 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-397">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following Match conditions: Edge Cname, Request Header Literal, Request Header Wildcard, URL Query Literal, and URL Query Wildcard.</span></span>

<span data-ttu-id="18385-398">값</span><span class="sxs-lookup"><span data-stu-id="18385-398">Value</span></span>|<span data-ttu-id="18385-399">결과</span><span class="sxs-lookup"><span data-stu-id="18385-399">Result</span></span>
--|--
<span data-ttu-id="18385-400">사용</span><span class="sxs-lookup"><span data-stu-id="18385-400">Enabled</span></span>|<span data-ttu-id="18385-401">Hello 기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-401">Restores hello default behavior.</span></span> <span data-ttu-id="18385-402">hello 기본 동작은 tooforce hello edge 서버 tooinitiate hello 원본 서버에서 hello 자산의 백그라운드 가져오기입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-402">hello default behavior is tooforce hello edge server tooinitiate a background fetch of hello asset from hello origin server.</span></span> <span data-ttu-id="18385-403">그 후 hello 자산 hello 지 서버 로컬 캐시에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-403">After which, hello asset will be in hello edge server's local cache.</span></span>
<span data-ttu-id="18385-404">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-404">Disabled</span></span>|<span data-ttu-id="18385-405">에 지 서버를 hello 자산에 대 한 백그라운드 가져오기를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-405">Prevents an edge server from performing a background fetch for hello asset.</span></span> <span data-ttu-id="18385-406">즉, 해당 hello 다음 요청 edge 서버 toorequest 하면 해당 지역에서 해당 자산에 대 한 hello 고객 원본 서버에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-406">This means that hello next request for that asset from that region will cause an edge server toorequest it from hello customer origin server.</span></span>

<span data-ttu-id="18385-407">**기본 동작**: 사용</span><span class="sxs-lookup"><span data-stu-id="18385-407">**Default Behavior:** Enabled.</span></span>

###<a name="compress-file-types"></a><span data-ttu-id="18385-408">압축 파일 형식</span><span class="sxs-lookup"><span data-stu-id="18385-408">Compress File Types</span></span>
<span data-ttu-id="18385-409">**목적:** hello 서버에서 압축 되도록 하는 hello 파일 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-409">**Purpose:** Defines hello file formats that will be compressed on hello server.</span></span>

<span data-ttu-id="18385-410">파일 형식은 인터넷 미디어 유형, 즉 Content-Type을 사용하여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-410">A file format can be specified using its Internet media type (i.e., Content-Type).</span></span> <span data-ttu-id="18385-411">인터넷 미디어 유형은 특정 자산 우리의 서버 tooidentify hello 파일 형식을 허용 하는 플랫폼 독립적 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-411">Internet media type is platform-independent metadata that allows our servers tooidentify hello file format of a particular asset.</span></span> <span data-ttu-id="18385-412">일반적인 인터넷 미디어 유형 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-412">A list of common Internet media types is provided below.</span></span>

<span data-ttu-id="18385-413">인터넷 미디어 유형</span><span class="sxs-lookup"><span data-stu-id="18385-413">Internet Media Type</span></span>|<span data-ttu-id="18385-414">설명</span><span class="sxs-lookup"><span data-stu-id="18385-414">Description</span></span>
--|--
<span data-ttu-id="18385-415">텍스트/일반</span><span class="sxs-lookup"><span data-stu-id="18385-415">text/plain</span></span>|<span data-ttu-id="18385-416">일반 텍스트 파일</span><span class="sxs-lookup"><span data-stu-id="18385-416">Plain text files</span></span>
<span data-ttu-id="18385-417">텍스트/html</span><span class="sxs-lookup"><span data-stu-id="18385-417">text/html</span></span>| <span data-ttu-id="18385-418">HTML 파일</span><span class="sxs-lookup"><span data-stu-id="18385-418">HTML files</span></span>
<span data-ttu-id="18385-419">텍스트/css</span><span class="sxs-lookup"><span data-stu-id="18385-419">text/css</span></span>|<span data-ttu-id="18385-420">CSS(스타일시트)</span><span class="sxs-lookup"><span data-stu-id="18385-420">Cascading Style Sheets (CSS)</span></span>
<span data-ttu-id="18385-421">application/x-javascript</span><span class="sxs-lookup"><span data-stu-id="18385-421">application/x-javascript</span></span>|<span data-ttu-id="18385-422">JavaScript</span><span class="sxs-lookup"><span data-stu-id="18385-422">Javascript</span></span>
<span data-ttu-id="18385-423">application/javascript</span><span class="sxs-lookup"><span data-stu-id="18385-423">application/javascript</span></span>|<span data-ttu-id="18385-424">JavaScript</span><span class="sxs-lookup"><span data-stu-id="18385-424">Javascript</span></span>
<span data-ttu-id="18385-425">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-425">Key information:</span></span>

- <span data-ttu-id="18385-426">각각 하나의 공백으로 구분하여 여러 인터넷 미디어 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-426">Specify multiple Internet media types by delimiting each one with a single space.</span></span> 
- <span data-ttu-id="18385-427">이 기능은 1MB 미만 크기의 자산만 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-427">This feature will only compress assets whose size is less than 1 MB.</span></span> <span data-ttu-id="18385-428">더 큰 자산은 서버에서 압축하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-428">Larger assets will not be compressed by our servers.</span></span>
- <span data-ttu-id="18385-429">이미지, 비디오 및 오디오 미디어 자산(예: JPG, MP3, MP4 등)과 같은 특정 유형의 콘텐츠는 이미 압축되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-429">Certain types of content, such as images, video, and audio media assets (e.g., JPG, MP3, MP4, etc.), are already compressed.</span></span> <span data-ttu-id="18385-430">이러한 유형의 자산을 추가로 압축해도 파일 크기가 크게 줄어들지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-430">Additional compression on these types of assets will not significantly diminish file size.</span></span> <span data-ttu-id="18385-431">따라서 이러한 유형의 자산에는 압축을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-431">Therefore, it is recommended that you do not enable compression on these types of assets.</span></span>
- <span data-ttu-id="18385-432">별표와 같은 와일드카드 문자는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-432">Wildcard characters, such as asterisks, are not supported.</span></span>
- <span data-ttu-id="18385-433">이 기능은 tooa 규칙을 추가 하기 전에 hello 플랫폼 toowhich이이 규칙은 적용에 대 한 압축 페이지 압축 사용 안 함 옵션 tooset 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-433">Before adding this feature tooa rule, make sure tooset the Compression Disabled option on the Compression page for hello platform toowhich this rule will be applied.</span></span>

###<a name="default-internal-max-age"></a><span data-ttu-id="18385-434">기본 내부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="18385-434">Default Internal Max-Age</span></span>
<span data-ttu-id="18385-435">**목적:** edge 서버 tooorigin 서버 캐시 유효성 재검사 Determines hello 기본 최대 처리 기간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-435">**Purpose:** Determines hello default max-age interval for edge server tooorigin server cache revalidation.</span></span> <span data-ttu-id="18385-436">즉, 앞에 지 서버에 전달 하는 시간의 양을 hello는 캐시 된 자산 hello 원본 서버에 저장 된 hello 자산 일치 하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-436">In other words, hello amount of time that will pass before an edge server will check whether a cached asset matches hello asset stored on hello origin server.</span></span>

<span data-ttu-id="18385-437">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-437">Key information:</span></span>

- <span data-ttu-id="18385-438">이 작업은 Cache-Control 또는 Expires 헤더에 max-age 표시를 할당하지 않은 원본 서버의 응답에 대해서만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-438">This action will only take place for responses from an origin server that did not assign a max-age indication in the Cache-Control or Expires header.</span></span>
- <span data-ttu-id="18385-439">이 작업은 캐시 가능하다고 간주되지 않는 자산에 대해서는 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-439">This action will not take place for assets that are not deemed cacheable.</span></span>
- <span data-ttu-id="18385-440">이 작업에는 브라우저 tooedge 서버 캐시 revalidations 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-440">This action does not affect browser tooedge server cache revalidations.</span></span> <span data-ttu-id="18385-441">이러한 유형의 revalidations 캐시 컨트롤에 의해 결정 됩니다 또는 Expires 헤더가 전송 toohello 브라우저 외부 Max-age 기능을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-441">These types of revalidations are determined by the Cache-Control or Expires headers sent toohello browser, which can be customized with the External Max-Age feature.</span></span>
- <span data-ttu-id="18385-442">이 동작의 결과가 hello hello 응답 헤더 및 콘텐츠에에 지 서버에서 반환 된 hello 콘텐츠에 눈에 띄는 영향 필요는 없지만 것에 지 서버 tooyour 원본 서버에서 보낸 유효성 재검사 트래픽의 hello 금액에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-442">hello results of this action do not have an observable effect on hello response headers and hello content returned from edge servers for your content, but it may have an effect on hello amount of revalidation traffic sent from edge servers tooyour origin server.</span></span>
- <span data-ttu-id="18385-443">이 기능은 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-443">Configure this feature by:</span></span>
    - <span data-ttu-id="18385-444">기본 내부 최대 보존 기간을 적용할 수 있는 hello 상태 코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-444">Selecting hello status code for which a default internal max-age can be applied.</span></span>
    - <span data-ttu-id="18385-445">정수 값을 지정 하 고 다음을 선택 하는 원하는 시간 단위 (예: 초, 분, 시간 등) hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-445">Specifying an integer value and then selecting hello desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="18385-446">이 값 hello 기본 내부 최대 처리 기간 간격을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-446">This value defines hello default internal max-age interval.</span></span>

- <span data-ttu-id="18385-447">설정 hello 시간 단위 너무 "Off"가 할당 Cache-control 또는 Expires 헤더에는 최대 기간 표시 할당 되지 않은 요청에 대 한 일의 기본 내부 최대 처리 기간 간격 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-447">Setting hello time unit too"Off" will assign a default internal max-age interval of 7 days for requests that have not been assigned a max-age indication in their Cache-Control or Expires header.</span></span>
- <span data-ttu-id="18385-448">설정을 추적 되는 캐시에 toohello 방식으로 인해 일치 조건을 다음 hello로이 기능은 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-448">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following match conditions:</span></span> 
    - <span data-ttu-id="18385-449">Edge</span><span class="sxs-lookup"><span data-stu-id="18385-449">Edge</span></span> 
    - <span data-ttu-id="18385-450">Cname</span><span class="sxs-lookup"><span data-stu-id="18385-450">Cname</span></span>
    - <span data-ttu-id="18385-451">요청 헤더 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-451">Request Header Literal</span></span>
    - <span data-ttu-id="18385-452">요청 헤더 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-452">Request Header Wildcard</span></span>
    - <span data-ttu-id="18385-453">요청 메서드</span><span class="sxs-lookup"><span data-stu-id="18385-453">Request Method</span></span>
    - <span data-ttu-id="18385-454">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-454">URL Query Literal</span></span>
    - <span data-ttu-id="18385-455">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-455">URL Query Wildcard</span></span>

<span data-ttu-id="18385-456">**기본값:** 7일</span><span class="sxs-lookup"><span data-stu-id="18385-456">**Default Value:** 7 days</span></span>

###<a name="expires-header-treatment"></a><span data-ttu-id="18385-457">만료 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="18385-457">Expires Header Treatment</span></span>
<span data-ttu-id="18385-458">**목적:** 외부 Max-age 기능이 활성화 되어 있을 때에 지 서버에서 Expires 헤더의 hello 생성을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-458">**Purpose:** Controls hello generation of Expires headers by an edge server when the External Max-Age feature is active.</span></span>

<span data-ttu-id="18385-459">이 구성 유형은 tooplace hello 외부 Max-age 및 hello 만료 헤더 처리 기능에는 가장 쉬운 방법은 tooachieve hello 동일한 문에서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-459">hello easiest way tooachieve this type of configuration is tooplace hello External Max-Age and hello Expires Header Treatment features in hello same statement.</span></span>

<span data-ttu-id="18385-460">값</span><span class="sxs-lookup"><span data-stu-id="18385-460">Value</span></span>|<span data-ttu-id="18385-461">결과</span><span class="sxs-lookup"><span data-stu-id="18385-461">Result</span></span>
--|--
<span data-ttu-id="18385-462">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-462">Overwrite</span></span>|<span data-ttu-id="18385-463">해당 hello 다음 작업 수행을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-463">Ensures that hello following actions will take place:</span></span><br/><span data-ttu-id="18385-464">-Hello 원본 서버에 의해 생성 된 Expires 헤더를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="18385-464">- Overwrites the Expires header generated by hello origin server.</span></span><br/><span data-ttu-id="18385-465">-Hello 외부 Max-age 기능 toohello 응답에서 생성 된 Expires 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-465">- Adds the Expires header produced by hello External Max-Age feature toohello response.</span></span>
<span data-ttu-id="18385-466">통과</span><span class="sxs-lookup"><span data-stu-id="18385-466">Pass Through</span></span>|<span data-ttu-id="18385-467">Expires 헤더 hello 외부 Max-age 기능에 의해 생성 된 toohello 응답 하지 않습니다 추가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-467">Ensures that the Expires header produced by hello External Max-Age feature is never added toohello response.</span></span> <br/> <span data-ttu-id="18385-468">Expires 헤더 생성 하는 원본 서버 hello toohello 최종 사용자를 통해 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-468">If hello origin server produces an Expires header, it will pass through toohello end-user.</span></span> <br/><span data-ttu-id="18385-469">원본 서버 hello Expires 헤더로, 다음이 옵션을 생성 하지 않으므로 포함 될 수 있습니다 원인 hello 응답 헤더 toonot Expires 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-469">If hello origin server does not produce an Expires header, then this option may cause hello response header toonot contain an Expires header.</span></span>
<span data-ttu-id="18385-470">없는 경우 추가</span><span class="sxs-lookup"><span data-stu-id="18385-470">Add if Missing</span></span>| <span data-ttu-id="18385-471">Expires 헤더 hello 원본 서버에서 수신 되지 않았습니다,이 옵션 hello 외부 Max-age 기능에 의해 생성 된 Expires 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-471">If an Expires header was not received from hello origin server, then this option adds the Expires header produced by hello External Max-Age feature.</span></span> <span data-ttu-id="18385-472">이 옵션은 모든 자산에 Expires 헤더를 할당하도록 하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-472">This option is useful for ensuring that all assets will be assigned an Expires header.</span></span>
<span data-ttu-id="18385-473">제거</span><span class="sxs-lookup"><span data-stu-id="18385-473">Remove</span></span>| <span data-ttu-id="18385-474">Expires 헤더 hello 헤더 응답에 포함 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-474">Ensures that an Expires header is not included with hello header response.</span></span> <span data-ttu-id="18385-475">Expires 헤더에 이미 할당 된 경우 다음 것에서 제거 됩니다 hello 헤더 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-475">If an Expires header has already been assigned, then it will be stripped from hello header response.</span></span>

<span data-ttu-id="18385-476">**기본 동작:** 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-476">**Default Behavior:** Overwrite</span></span>

###<a name="external-max-age"></a><span data-ttu-id="18385-477">외부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="18385-477">External Max-Age</span></span>
<span data-ttu-id="18385-478">**목적:** 브라우저 tooedge 서버 캐시 유효성 재검사 hello 최대 처리 기간 간격을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-478">**Purpose:** Determines hello max-age interval for browser tooedge server cache revalidation.</span></span> <span data-ttu-id="18385-479">즉, 새 버전의 자산을에 지 서버 hello 브라우저 전에 전달 하는 시간의 양을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-479">In other words, hello amount of time that will pass before a browser can check for a new version of an asset from an edge server.</span></span>

<span data-ttu-id="18385-480">이 기능을 사용 하면 캐시를 생성 합니다-제어: 최대-age 및 헤더는에 지 서버에서 만료 되 고 보내는 toohello HTTP 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-480">Enabling this feature will generate Cache-Control:max-age and Expires headers from our edge servers and send them toohello HTTP client.</span></span> <span data-ttu-id="18385-481">이러한 헤더는 기본적으로 hello 원본 서버에서 만든를 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-481">By default, these headers will overwrite those created by hello origin server.</span></span> <span data-ttu-id="18385-482">그러나 캐시 컨트롤 헤더 처리 및 헤더 처리 만료 기능 수 있습니다이 동작은 사용 되는 tooalter 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-482">However, the Cache-Control Header Treatment and the Expires Header Treatment features may be used tooalter this behavior.</span></span>

<span data-ttu-id="18385-483">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-483">Key information:</span></span>

- <span data-ttu-id="18385-484">이 작업에 지 서버 tooorigin 서버 캐시 revalidations 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-484">This action does not affect edge server tooorigin server cache revalidations.</span></span> <span data-ttu-id="18385-485">이러한 유형의 revalidations hello 원본 서버에서 받은 캐시-컨트롤/Expires 헤더에 의해 결정 됩니다 하 고는 기본 내부 Max-age 및 Force 내부 Max-age 기능으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-485">These types of revalidations are determined by the Cache-Control/Expires headers received from hello origin server, and can be customized with the Default Internal Max-Age and the Force Internal Max-Age features.</span></span>
- <span data-ttu-id="18385-486">정수 값을 지정 하 고 hello 원하는 시간 단위 (예: 초, 분, 시간 등)를 선택 하 여이 기능을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-486">Configure this feature by specifying an integer value and selecting hello desired time unit (i.e., seconds, minutes, hours, etc.).</span></span>
- <span data-ttu-id="18385-487">이 기능은 tooa 음수 값을 설정 하면 우리의 edge 서버 toosend 캐시-제어: no-캐시 및 hello에 설정 된 만료 시간 각 응답 toohello 브라우저와 과거 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-487">Setting this feature tooa negative value causes our edge servers toosend a Cache-Control:no-cache and an Expires time that is set in hello past with each response toohello browser.</span></span> <span data-ttu-id="18385-488">HTTP 클라이언트 hello 응답을 캐시 하지 않습니다, 하지만이 설정은 edge 서버 기능 toocache hello 응답 hello 원본 서버에서 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-488">Although an HTTP client will not cache hello response, this setting will not affect our edge servers' ability toocache hello response from hello origin server.</span></span>
- <span data-ttu-id="18385-489">설정 hello 시간 단위 너무 "Off"는이 기능을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-489">Setting hello time unit too"Off" will disable this feature.</span></span> <span data-ttu-id="18385-490">Hello hello 원본 서버에 대 한 응답으로 캐시는 캐시-컨트롤/Expires 헤더 toohello 브라우저를 통해 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-490">The Cache-Control/Expires headers cached with hello response of hello origin server will pass through toohello browser.</span></span>

<span data-ttu-id="18385-491">**기본 동작:** 끄기</span><span class="sxs-lookup"><span data-stu-id="18385-491">**Default Behavior:** Off</span></span>

###<a name="force-internal-max-age"></a><span data-ttu-id="18385-492">강제 내부 Max-Age</span><span class="sxs-lookup"><span data-stu-id="18385-492">Force Internal Max-Age</span></span>
<span data-ttu-id="18385-493">**목적:** edge 서버 tooorigin 서버 캐시 유효성 재검사 hello 최대 처리 기간 간격을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-493">**Purpose:** Determines hello max-age interval for edge server tooorigin server cache revalidation.</span></span> <span data-ttu-id="18385-494">즉, 앞에 지 서버에 전달 하는 시간의 양을 hello 캐시 된 자산 hello 원본 서버에 저장 된 hello 자산 일치 하는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-494">In other words, hello amount of time that will pass before an edge server can check whether a cached asset matches hello asset stored on hello origin server.</span></span>

<span data-ttu-id="18385-495">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-495">Key information:</span></span>

- <span data-ttu-id="18385-496">이 기능은 Cache-control 또는 Expires 헤더는 원본 서버에서 생성 된에 정의 된 hello 최대 처리 기간 간격을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-496">This feature will override hello max-age interval defined in Cache-Control or Expires headers generated from an origin server.</span></span>
- <span data-ttu-id="18385-497">이 기능은 브라우저 tooedge 서버 캐시 revalidations 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-497">This feature does not affect browser tooedge server cache revalidations.</span></span> <span data-ttu-id="18385-498">이러한 유형의 revalidations 캐시 컨트롤에 의해 결정 됩니다 또는 Expires 헤더가 toohello 브라우저를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-498">These types of revalidations are determined by the Cache-Control or Expires headers sent toohello browser.</span></span>
- <span data-ttu-id="18385-499">이 기능에는 edge 서버 toohello 요청자에서 제공 하는 hello 응답에는 observable 효과가지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-499">This feature does not have an observable effect on hello response delivered by an edge server toohello requester.</span></span> <span data-ttu-id="18385-500">그러나 우리 지 서버 toohello 원본 서버에서 보낸 유효성 재검사 트래픽의 hello 금액에 영향을 미칠 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-500">However, it may have an effect on hello amount of revalidation traffic sent from our edge servers toohello origin server.</span></span>
- <span data-ttu-id="18385-501">이 기능은 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-501">Configure this feature by:</span></span>
    - <span data-ttu-id="18385-502">내부 최대 기간을 적용할 hello 상태 코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-502">Selecting hello status code for which an internal max-age will be applied.</span></span>
    - <span data-ttu-id="18385-503">정수 값을 지정 하 고 선택 하면 hello 원하는 시간 단위 (예: 초, 분, 시간 등).</span><span class="sxs-lookup"><span data-stu-id="18385-503">Specifying an integer value and selecting hello desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="18385-504">이 값 hello 요청 최대 처리 기간 간격을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-504">This value defines hello request's max-age interval.</span></span>

- <span data-ttu-id="18385-505">설정 hello 시간 단위 너무 "Off"이이 기능이 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-505">Setting hello time unit too"Off" disables this feature.</span></span> <span data-ttu-id="18385-506">내부 최대 처리 기간 간격 toorequested 자산 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-506">An internal max-age interval will not be assigned toorequested assets.</span></span> <span data-ttu-id="18385-507">Hello 원래 머리글 캐싱 지침을 포함 하지 않으면 hello 자산 toohello 기본 내부 Max-age 기능에서 활성 설정에 따라 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-507">If hello original header does not contain caching instructions, then hello asset will be cached according toohello active setting in the Default Internal Max-Age feature.</span></span>
- <span data-ttu-id="18385-508">설정을 추적 되는 캐시에 toohello 방식으로 인해 일치 조건을 다음 hello로이 기능은 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-508">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following match conditions:</span></span> 
    - <span data-ttu-id="18385-509">Edge</span><span class="sxs-lookup"><span data-stu-id="18385-509">Edge</span></span> 
    - <span data-ttu-id="18385-510">Cname</span><span class="sxs-lookup"><span data-stu-id="18385-510">Cname</span></span>
    - <span data-ttu-id="18385-511">요청 헤더 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-511">Request Header Literal</span></span>
    - <span data-ttu-id="18385-512">요청 헤더 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-512">Request Header Wildcard</span></span>
    - <span data-ttu-id="18385-513">요청 메서드</span><span class="sxs-lookup"><span data-stu-id="18385-513">Request Method</span></span>
    - <span data-ttu-id="18385-514">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-514">URL Query Literal</span></span>
    - <span data-ttu-id="18385-515">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-515">URL Query Wildcard</span></span>

<span data-ttu-id="18385-516">**기본 동작:** 끄기</span><span class="sxs-lookup"><span data-stu-id="18385-516">**Default Behavior:** Off</span></span>

###<a name="h264-support-http-progressive-download"></a><span data-ttu-id="18385-517">H.264 지원(HTTP 점진적 다운로드)</span><span class="sxs-lookup"><span data-stu-id="18385-517">H.264 Support (HTTP Progressive Download)</span></span>
<span data-ttu-id="18385-518">**목적:** Determines hello 유형의 H.264 파일 형식을 사용 하는 toostream 수 있는 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-518">**Purpose:** Determines hello types of H.264 file formats that may be used toostream content.</span></span>

<span data-ttu-id="18385-519">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-519">Key information:</span></span>

- <span data-ttu-id="18385-520">파일 확장명 옵션에서 허용되는 H.264 파일 이름 확장명의 공백으로 구분된 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-520">Define a space-delimited set of allowed H.264 filename extensions in the File Extensions option.</span></span> <span data-ttu-id="18385-521">파일 확장명 옵션 hello 기본 동작을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-521">The File Extensions option will override hello default behavior.</span></span> <span data-ttu-id="18385-522">이 옵션을 설정할 때 파일 이름 확장명을 포함하여 MP4 및 F4V 지원을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-522">Maintain MP4 and F4V support by including those filename extensions when setting this option.</span></span> 
- <span data-ttu-id="18385-523">있는지 tooinclude 기간을 확인 하십시오. 각 파일 이름 확장명 (예:.mp4.f4v)를 지정 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="18385-523">Make sure tooinclude a period when specifying each filename extension (e.g., .mp4 .f4v).</span></span>

<span data-ttu-id="18385-524">**기본 동작:** HTTP 점진적 다운로드는 기본적으로 MP4 및 F4V 미디어를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-524">**Default Behavior:** HTTP Progressive Download supports MP4 and F4V media by default.</span></span>

###<a name="honor-no-cache-request"></a><span data-ttu-id="18385-525">no-cache 요청 부여</span><span class="sxs-lookup"><span data-stu-id="18385-525">Honor no-cache request</span></span>
<span data-ttu-id="18385-526">**목적:** 여부는 HTTP 클라이언트의 캐시 없음 요청 toohello 원본 서버를 전달 됩니다 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-526">**Purpose:** Determines whether an HTTP client's no-cache requests will be forwarded toohello origin server.</span></span>

<span data-ttu-id="18385-527">No 캐시 요청 발생 hello HTTP 클라이언트에서 캐시를 보낼 때-제어: no-캐시 및/또는 Pragma:no-hello HTTP 요청에 캐시 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-527">A no-cache request occurs when hello HTTP client sends a Cache-Control:no-cache and/or Pragma:no-cache header in hello HTTP request.</span></span>

<span data-ttu-id="18385-528">값</span><span class="sxs-lookup"><span data-stu-id="18385-528">Value</span></span>|<span data-ttu-id="18385-529">결과</span><span class="sxs-lookup"><span data-stu-id="18385-529">Result</span></span>
--|--
<span data-ttu-id="18385-530">사용</span><span class="sxs-lookup"><span data-stu-id="18385-530">Enabled</span></span>|<span data-ttu-id="18385-531">HTTP 클라이언트의 아니요 캐시 toobe 전달된 toohello 원본 서버를 요청 하 고 hello 원본 서버는 반환 hello 응답 헤더 및 hello 본문 hello 지 서버를 통해 백 toohello HTTP 클라이언트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-531">Allows an HTTP client's no-cache requests toobe forwarded toohello origin server, and hello origin server will return hello response headers and hello body through hello edge server back toohello HTTP client.</span></span>
<span data-ttu-id="18385-532">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-532">Disabled</span></span>|<span data-ttu-id="18385-533">Hello 기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-533">Restores hello default behavior.</span></span> <span data-ttu-id="18385-534">hello 기본 동작은 원본 서버에 toohello 전달을 tooprevent 아니요 캐시 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-534">hello default behavior is tooprevent no-cache requests from being forwarded toohello origin server.</span></span>

<span data-ttu-id="18385-535">모든 프로덕션 트래픽에 대 한 것은 매우 tooleave 사용 하지 않도록 설정 하는 기본 상태에서이 기능을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-535">For all production traffic, it is highly recommended tooleave this feature in its default disabled state.</span></span> <span data-ttu-id="18385-536">그렇지 않은 경우 원본 서버에서 최종 사용자 웹 페이지를 새로 고칠 때 많은 아니요 캐시 요청을 실수로 트리거될 수 있습니다 보호 하지 않습니다 또는 hello에서 인기 있는 미디어 플레이어 있는 코딩 된 toosend 아니요 캐시 헤더 비디오 모든 요청에 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-536">Otherwise, origin servers will not be shielded from end-users who may inadvertently trigger many no-cache requests when refreshing web pages, or from hello many popular media players that are coded toosend a no-cache header with every video request.</span></span> <span data-ttu-id="18385-537">그럼에도 불구 하 고이 기능은 유용 tooapply toocertain 비-프로덕션 준비 수 또는 요청 시 hello 원본 서버에서 끌어온 순서 tooallow 새 콘텐츠 toobe에서 디렉터리를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-537">Nevertheless, this feature can be useful tooapply toocertain non-production staging or testing directories, in order tooallow fresh content toobe pulled on-demand from hello origin server.</span></span>

<span data-ttu-id="18385-538">toothis 기능 인해 전달 toobe tooan 원본 서버는 TCP_Client_Refresh_Miss 허용 되는 요청에 대 한 보고 되는 hello 캐시 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-538">hello cache status that will be reported for a request that is allowed toobe forwarded tooan origin server due toothis feature is TCP_Client_Refresh_Miss.</span></span> <span data-ttu-id="18385-539">Hello 핵심 보고 모듈에서 사용할 수 있는 캐시 상태 보고서 캐시 상태에 의해 통계 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-539">The Cache Statuses report, which is available in hello Core reporting module, provides statistical information by cache status.</span></span> <span data-ttu-id="18385-540">이렇게 하면 tootrack hello 번호와 요청 비율을 toothis 기능 인해 tooan 원본 서버에 전달 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-540">This allows you tootrack hello number and percentage of requests that are being forwarded tooan origin server due toothis feature.</span></span>

<span data-ttu-id="18385-541">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-541">**Default Behavior:** Disabled.</span></span>

###<a name="ignore-origin-no-cache"></a><span data-ttu-id="18385-542">원본 no-cache 무시</span><span class="sxs-lookup"><span data-stu-id="18385-542">Ignore Origin no-cache</span></span>
<span data-ttu-id="18385-543">**목적:** 우리의 CDN은 hello 원본 서버에서 제공 하는 지시문 뒤를 무시 하는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-543">**Purpose:** Determines whether our CDN will ignore hello following directives served from an origin server:</span></span>

- <span data-ttu-id="18385-544">Cache-Control: private</span><span class="sxs-lookup"><span data-stu-id="18385-544">Cache-Control: private</span></span>
- <span data-ttu-id="18385-545">Cache-Control: no-store</span><span class="sxs-lookup"><span data-stu-id="18385-545">Cache-Control: no-store</span></span>
- <span data-ttu-id="18385-546">Cache-Control: no-cache</span><span class="sxs-lookup"><span data-stu-id="18385-546">Cache-Control: no-cache</span></span>
- <span data-ttu-id="18385-547">Pragma: no-cache</span><span class="sxs-lookup"><span data-stu-id="18385-547">Pragma: no-cache</span></span>

<span data-ttu-id="18385-548">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-548">Key information:</span></span>

- <span data-ttu-id="18385-549">공백으로 구분 된 목록이 지시문 위에 hello 무시 되는 상태 코드를 정의 하 여이 기능을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-549">Configure this feature by defining a space-delimited list of status codes for which hello above directives will be ignored.</span></span>
- <span data-ttu-id="18385-550">hello이 기능에 대 한 유효한 상태 코드의 집합은: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, 및 505 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-550">hello set of valid status codes for this feature are: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, and 505.</span></span>
- <span data-ttu-id="18385-551">Tooa 빈 값을 설정 하 여이 기능을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-551">Disable this feature by setting it tooa blank value.</span></span>
- <span data-ttu-id="18385-552">설정을 추적 되는 캐시에 toohello 방식으로 인해 일치 조건을 다음 hello로이 기능은 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-552">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following match conditions:</span></span> 
    - <span data-ttu-id="18385-553">Edge</span><span class="sxs-lookup"><span data-stu-id="18385-553">Edge</span></span> 
    - <span data-ttu-id="18385-554">Cname</span><span class="sxs-lookup"><span data-stu-id="18385-554">Cname</span></span>
    - <span data-ttu-id="18385-555">요청 헤더 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-555">Request Header Literal</span></span>
    - <span data-ttu-id="18385-556">요청 헤더 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-556">Request Header Wildcard</span></span>
    - <span data-ttu-id="18385-557">요청 메서드</span><span class="sxs-lookup"><span data-stu-id="18385-557">Request Method</span></span>
    - <span data-ttu-id="18385-558">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-558">URL Query Literal</span></span>
    - <span data-ttu-id="18385-559">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-559">URL Query Wildcard</span></span>

<span data-ttu-id="18385-560">**기본 동작:** 기본 동작은 지시문 위에 toohonor hello입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-560">**Default Behavior:** The default behavior is toohonor hello above directives.</span></span>

###<a name="ignore-unsatisfiable-ranges"></a><span data-ttu-id="18385-561">적절하지 않은 범위 무시</span><span class="sxs-lookup"><span data-stu-id="18385-561">Ignore Unsatisfiable Ranges</span></span> 
<span data-ttu-id="18385-562">**목적:** hello 응답 반환 되는 tooclients 요청 요청한 범위가 충분 하지 않음 416 상태 코드를 생성 하는 경우를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-562">**Purpose:** Determines hello response that will be returned tooclients when a request generates a 416 Requested Range Not Satisfiable status code.</span></span>

<span data-ttu-id="18385-563">기본적으로이 상태 코드는 바이트 범위 요청을에 지 서버에서 충족 되지 않습니다 및 If-range 요청 헤더 필드를 지정 하지 않았습니다 hello 지정 된 경우 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-563">By default, this status code is returned when hello specified byte-range request cannot be satisfied by an edge server and an If-Range request header field was not specified.</span></span>

<span data-ttu-id="18385-564">값</span><span class="sxs-lookup"><span data-stu-id="18385-564">Value</span></span>|<span data-ttu-id="18385-565">결과</span><span class="sxs-lookup"><span data-stu-id="18385-565">Result</span></span>
-|-
<span data-ttu-id="18385-566">사용</span><span class="sxs-lookup"><span data-stu-id="18385-566">Enabled</span></span>|<span data-ttu-id="18385-567">Edge 서버에서 요청한 범위가 충분 하지 않음 416 상태 코드로 응답 tooan 잘못 된 바이트 범위 요청을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-567">Prevents our edge servers from responding tooan invalid byte-range request with a 416 Requested Range Not Satisfiable status code.</span></span> <span data-ttu-id="18385-568">대신 서버 hello 요청한 자산 배달 하 고 200 OK hello 클라이언트로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-568">Instead our servers will deliver hello requested asset and return a 200 OK to hello client.</span></span>
<span data-ttu-id="18385-569">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-569">Disabled</span></span>|<span data-ttu-id="18385-570">Hello 기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-570">Restores hello default behavior.</span></span> <span data-ttu-id="18385-571">hello 기본 동작은 toohonor 요청한 범위가 충분 하지 않음 416 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-571">hello default behavior is toohonor the 416 Requested Range Not Satisfiable status code.</span></span>

<span data-ttu-id="18385-572">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-572">**Default Behavior:** Disabled.</span></span>

###<a name="internal-max-stale"></a><span data-ttu-id="18385-573">내부 Max-Stale</span><span class="sxs-lookup"><span data-stu-id="18385-573">Internal Max-Stale</span></span>
<span data-ttu-id="18385-574">**목적:** hello에 지 서버는 없습니다 toorevalidate hello 때 캐시 된 자산에 지 서버에서 구현 될 수 있습니다 지난 hello 정상적으로 종료 시간 hello 원본 서버와 자산을 캐시 하는 기간을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-574">**Purpose:** Controls how long past hello normal expiration time a cached asset may be served from an edge server when hello edge server is unable toorevalidate hello cached asset with hello origin server.</span></span>

<span data-ttu-id="18385-575">일반적으로 자산 최대 처리 기간 시간이 만료 되 면 hello에 지 서버 유효성 재검사 요청 toohello 원본 서버를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-575">Normally, when an asset's max-age time expires, hello edge server will send a revalidation request toohello origin server.</span></span> <span data-ttu-id="18385-576">hello 원본 서버는 다음으로 응답 중 하나는 304 귀하에 게 hello에 지 서버 새로운 임대를 200으로 그렇지 않으면 hello 캐시 된 자산에 대해 확인 hello에 지 서버 hello 캐시 된 asset의 업데이트 된 버전 제공 수정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-576">hello origin server will then respond with either a 304 Not Modified to give hello edge server a fresh lease on hello cached asset, or else with 200 OK to provide hello edge server with an updated version of hello cached asset.</span></span>

<span data-ttu-id="18385-577">Hello에 지 서버에 없습니다 tooestablish 이러한 유효성 재검사를 시도 하는 동안 hello 원본 서버와의 연결을 경우이 내부 최대 부실 기능에 지 서버 tooserve hello 지금 부실 자산 계속 수 있는지 여부와 시간, hello에 대 한 제어 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-577">If hello edge server is unable tooestablish a connection with hello origin server while attempting such a revalidation, then this Internal Max-Stale feature controls whether, and for how long, hello edge server may continue tooserve hello now-stale asset.</span></span>

<span data-ttu-id="18385-578">Note hello 실패 한 유효성 재검사 발생 때가 아니라 hello 자산 최대 처리 기간 만료 되 면이 시간 간격은 시작 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-578">Note that this time interval starts when hello asset's max-age expires, not when hello failed revalidation occurs.</span></span> <span data-ttu-id="18385-579">따라서는 자산 제공 될 수 있지만 유효성 재검사 없이 hello 최대 기간은 경우 hello 시간 최대 처리 기간을 더한 최대 부실 hello 조합 하 여 지정 된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-579">Therefore, hello maximum period during which an asset can be served without successful revalidation is hello amount of time specified by hello combination of max-age plus max-stale.</span></span> <span data-ttu-id="18385-580">예를 들어 자산에 실패 한 유효성을 다시 시도 9 시 30 분의 최대 기간 및 최대 부실 15 분에 캐시 된 경우 9시 44분 초래 최종 사용자 수신 hello 오래 된 캐시 된 자산을 9시 46분 한 실패 한 유효성을 다시 시도 초래 하는 동안 hello 최종 사용자 504 게이트웨이 시간 초과 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-580">For example, if an asset was cached at 9:00 with a max-age of 30 minutes and a max-stale of 15 minutes, then a failed revalidation attempt at 9:44 would result in an end-user receiving hello stale cached asset, while a failed revalidation attempt at 9:46 would result in hello end user receiving a 504 Gateway Timeout.</span></span>

<span data-ttu-id="18385-581">캐시에 의해 교체 된이 기능에 대해 구성 된 모든 값-제어: 해야-유효성을 다시 검사 또는 캐시-제어: 프록시-hello 원본 서버에서 받은 헤더 다시 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-581">Any value configured for this feature is superseded by Cache-Control:must-revalidate or Cache-Control:proxy-revalidate headers received from hello origin server.</span></span> <span data-ttu-id="18385-582">이러한 헤더 중 하나는 자산의 캐시 처음 되 면 hello 원본 서버에서 수신 되 면 hello edge 서버에는 오래 된 캐시 된 자산 하지 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-582">If either of those headers is received from hello origin server when an asset is initially cached, then hello edge server will not serve a stale cached asset.</span></span> <span data-ttu-id="18385-583">이 경우 중이면 hello에 지 서버 hello 원점으로 수 없습니다 toorevalidate hello 자산 최대 처리 기간 간격이 만료 되 면 다음 hello에 지 서버는 반환 504 게이트웨이 시간 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-583">In such a case, if hello edge server is unable toorevalidate with hello origin when hello asset's max-age interval has expired, then hello edge server will return a 504 Gateway Timeout.</span></span>

<span data-ttu-id="18385-584">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-584">Key information:</span></span>

- <span data-ttu-id="18385-585">이 기능은 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-585">Configure this feature by:</span></span>
    - <span data-ttu-id="18385-586">최대 부실 적용할 수 hello 상태 코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-586">Selecting hello status code for which a max-stale will be applied.</span></span>
    - <span data-ttu-id="18385-587">정수 값을 지정 하 고 다음을 선택 하는 원하는 시간 단위 (예: 초, 분, 시간 등) hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-587">Specifying an integer value and then selecting hello desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="18385-588">Hello 내부 최대-부실 적용 되는이 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-588">This value defines hello internal max-stale that will be applied.</span></span>

- <span data-ttu-id="18385-589">설정 hello 시간 단위 너무 "Off"는이 기능을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-589">Setting hello time unit too"Off" will disable this feature.</span></span> <span data-ttu-id="18385-590">캐시된 자산은 정상 만료 시간을 초과하여 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-590">A cached asset will not be served beyond its normal expiration time.</span></span>
- <span data-ttu-id="18385-591">설정을 추적 되는 캐시에 toohello 방식으로 인해 일치 조건을 다음 hello로이 기능은 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-591">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following match conditions:</span></span> 
    - <span data-ttu-id="18385-592">Edge</span><span class="sxs-lookup"><span data-stu-id="18385-592">Edge</span></span> 
    - <span data-ttu-id="18385-593">Cname</span><span class="sxs-lookup"><span data-stu-id="18385-593">Cname</span></span>
    - <span data-ttu-id="18385-594">요청 헤더 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-594">Request Header Literal</span></span>
    - <span data-ttu-id="18385-595">요청 헤더 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-595">Request Header Wildcard</span></span>
    - <span data-ttu-id="18385-596">요청 메서드</span><span class="sxs-lookup"><span data-stu-id="18385-596">Request Method</span></span>
    - <span data-ttu-id="18385-597">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-597">URL Query Literal</span></span>
    - <span data-ttu-id="18385-598">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-598">URL Query Wildcard</span></span>

<span data-ttu-id="18385-599">**기본 동작:** 2분</span><span class="sxs-lookup"><span data-stu-id="18385-599">**Default Behavior:** 2 minutes</span></span>

###<a name="partial-cache-sharing"></a><span data-ttu-id="18385-600">부분 캐시 공유</span><span class="sxs-lookup"><span data-stu-id="18385-600">Partial Cache Sharing</span></span>
<span data-ttu-id="18385-601">**목적:** 요청에서 부분적으로 캐시된 콘텐츠를 생성할 수 있는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-601">**Purpose:** Determines whether a request can generate partially cached content.</span></span>

<span data-ttu-id="18385-602">그런 다음이 부분 캐시는 hello 요청 콘텐츠가 캐시 되 고 완전 하 게 될 때까지 사용된 toofulfill 해당 콘텐츠에 대 한 새 요청을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-602">This partial cache may then be used toofulfill new requests for that content until hello requested content is fully cached.</span></span>

<span data-ttu-id="18385-603">값</span><span class="sxs-lookup"><span data-stu-id="18385-603">Value</span></span>|<span data-ttu-id="18385-604">결과</span><span class="sxs-lookup"><span data-stu-id="18385-604">Result</span></span>
-|-
<span data-ttu-id="18385-605">사용</span><span class="sxs-lookup"><span data-stu-id="18385-605">Enabled</span></span>|<span data-ttu-id="18385-606">요청에서 부분적으로 캐시된 콘텐츠를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-606">Requests can generate partially cached content.</span></span>
<span data-ttu-id="18385-607">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-607">Disabled</span></span>|<span data-ttu-id="18385-608">요청 캐시 된 완벽 하 게 생성할 수 버전의 hello 요청 되는 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-608">Requests can only generate a fully cached version of hello requested content.</span></span>

<span data-ttu-id="18385-609">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-609">**Default Behavior:** Disabled.</span></span>

###<a name="prevalidate-cached-content"></a><span data-ttu-id="18385-610">캐시된 콘텐츠 사전 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="18385-610">Prevalidate Cached Content</span></span>
<span data-ttu-id="18385-611">**목적:** TTL이 만료되기 전에 캐시된 콘텐츠가 초기 유효성 재검사에 적합한지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-611">**Purpose:** Determines whether cached content will be eligible for early revalidation before its TTL expires.</span></span>

<span data-ttu-id="18385-612">Hello 이전 toohello 만료 요청 콘텐츠의 TTL는 초기 유효성 재검사 적격 됩니다 시간의 hello 크기를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-612">Define hello amount of time prior toohello expiration of hello requested content's TTL during which it will be eligible for early revalidation.</span></span>

<span data-ttu-id="18385-613">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-613">Key information:</span></span>

- <span data-ttu-id="18385-614">유효성 재검사 tootake 위치 hello 캐시 된 콘텐츠의 TTL이 만료 된 후 필요 "Off" hello 시간 단위로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-614">Selecting "Off" as hello time unit requires revalidation tootake place after hello cached content's TTL has expired.</span></span> <span data-ttu-id="18385-615">시간은 지정하지 않아야 하며, 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-615">Time should not be specified and it will be ignored.</span></span>

<span data-ttu-id="18385-616">**기본 동작:** 끄기</span><span class="sxs-lookup"><span data-stu-id="18385-616">**Default Behavior:** Off.</span></span> <span data-ttu-id="18385-617">유효성 재검사 hello 캐시 된 콘텐츠의 TTL이 만료 된 후 수행만 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-617">Revalidation may only take place after hello cached content's TTL has expired.</span></span>

###<a name="refresh-zero-byte-cache-files"></a><span data-ttu-id="18385-618">0바이트 캐시 파일 새로 고침</span><span class="sxs-lookup"><span data-stu-id="18385-618">Refresh Zero Byte Cache Files</span></span>
<span data-ttu-id="18385-619">**목적:** 에지 서버에서 0바이트 캐시 자산에 대한 HTTP 클라이언트 요청을 처리하는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-619">**Purpose:** Determines how an HTTP client's request for a 0-byte cache asset is handled by our edge servers.</span></span>

<span data-ttu-id="18385-620">유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-620">Valid values are:</span></span>

<span data-ttu-id="18385-621">값</span><span class="sxs-lookup"><span data-stu-id="18385-621">Value</span></span>|<span data-ttu-id="18385-622">결과</span><span class="sxs-lookup"><span data-stu-id="18385-622">Result</span></span>
--|--
<span data-ttu-id="18385-623">사용</span><span class="sxs-lookup"><span data-stu-id="18385-623">Enabled</span></span>|<span data-ttu-id="18385-624">Edge 서버 toore 인출 hello 자산 hello 원본 서버에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-624">Causes our edge server toore-fetch hello asset from hello origin server.</span></span>
<span data-ttu-id="18385-625">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-625">Disabled</span></span>|<span data-ttu-id="18385-626">Hello 기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-626">Restores hello default behavior.</span></span> <span data-ttu-id="18385-627">hello 기본 동작은 요청에 따라 올바른 캐시 자산을 tooserve입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-627">hello default behavior is tooserve up valid cache assets upon request.</span></span>
<span data-ttu-id="18385-628">이 기능은 올바른 캐싱 및 콘텐츠 배달에는 필요하지 않지만 해결 방법으로는 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-628">This feature is not required for correct caching and content delivery, but may be useful as a workaround.</span></span> <span data-ttu-id="18385-629">예를 들어 원본 서버에서 동적 콘텐츠 생성기 toohello에 지 서버에 전송 되는 0 바이트 응답에서 실수로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-629">For example, dynamic content generators on origin servers can inadvertently result in 0-byte responses being sent toohello edge servers.</span></span> <span data-ttu-id="18385-630">이러한 유형의 응답은 일반적으로 에지 서버에서 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-630">These types of responses are typically cached by our edge servers.</span></span> <span data-ttu-id="18385-631">0바이트 응답이 이러한 콘텐츠에 대해 유효한 응답이 아님을 알고 있는 경우</span><span class="sxs-lookup"><span data-stu-id="18385-631">If you know that a 0-byte response is never a valid response</span></span> 

<span data-ttu-id="18385-632">신뢰할 수 없는 경우에 대 한 다음이 기능은 이러한 종류의 방지할 수 자산을 처리할 tooyour 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-632">for such content, then this feature can prevent these types of assets from being served tooyour clients.</span></span>

<span data-ttu-id="18385-633">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-633">**Default Behavior:** Disabled.</span></span>

###<a name="set-cacheable-status-codes"></a><span data-ttu-id="18385-634">캐시 가능한 상태 코드 집합</span><span class="sxs-lookup"><span data-stu-id="18385-634">Set Cacheable Status Codes</span></span>
<span data-ttu-id="18385-635">**목적:** 캐시 된 콘텐츠 발생할 수 있는 상태 코드의 hello 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-635">**Purpose:** Defines hello set of status codes that can result in cached content.</span></span>

<span data-ttu-id="18385-636">기본적으로 캐싱은 200 확인 응답에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-636">By default, caching is only enabled for 200 OK responses.</span></span>

<span data-ttu-id="18385-637">원하는 hello 상태 코드는 공백으로 구분 된 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-637">Define a space-delimited set of hello desired status codes.</span></span>

<span data-ttu-id="18385-638">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-638">Key information:</span></span>

- <span data-ttu-id="18385-639">원본 No-Cache 무시 기능도 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-639">Please also enable the Ignore Origin No-Cache feature.</span></span> <span data-ttu-id="18385-640">해당 기능을 사용할 수 없으면 비 200 확인 응답이 캐시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-640">If that feature is not enabled, then non-200 OK responses may not be cached.</span></span>
- <span data-ttu-id="18385-641">hello이 기능에 대 한 유효한 상태 코드의 집합은: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, 및 505 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-641">hello set of valid status codes for this feature are: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, and 505.</span></span>
- <span data-ttu-id="18385-642">이 기능에는 200 OK 상태 코드를 생성 하는 응답에 대 한 캐싱을 사용 하는 toodisable 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-642">This feature cannot be used toodisable caching for responses that generate a 200 OK status code.</span></span>

<span data-ttu-id="18385-643">**기본 동작:** 캐싱은 200 확인 상태 코드를 생성하는 응답에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-643">**Default Behavior:** Caching is only enabled for responses that generate a 200 OK status code.</span></span>
###<a name="stale-content-delivery-on-error"></a><span data-ttu-id="18385-644">오류 시 오래된 콘텐츠 배달</span><span class="sxs-lookup"><span data-stu-id="18385-644">Stale Content Delivery on Error</span></span>
<span data-ttu-id="18385-645">**목적:**</span><span class="sxs-lookup"><span data-stu-id="18385-645">**Purpose:**</span></span> 

<span data-ttu-id="18385-646">캐시 유효성 재검사 중 또는 검색 하는 동안 hello hello 고객 원본 서버에서 콘텐츠를 요청 하면 오류가 발생할 때 배달 될 캐시 된 콘텐츠 만료 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-646">Determines whether expired cached content will be delivered when an error occurs during cache revalidation or when retrieving hello requested content from hello customer origin server.</span></span>

<span data-ttu-id="18385-647">값</span><span class="sxs-lookup"><span data-stu-id="18385-647">Value</span></span>|<span data-ttu-id="18385-648">결과</span><span class="sxs-lookup"><span data-stu-id="18385-648">Result</span></span>
-|-
<span data-ttu-id="18385-649">사용</span><span class="sxs-lookup"><span data-stu-id="18385-649">Enabled</span></span>|<span data-ttu-id="18385-650">오래 된 콘텐츠는 제공 toohello 요청자 연결 tooan 원본 서버는 동안 오류가 발생 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="18385-650">Stale content will be served toohello requester when an error occurs during a connection tooan origin server.</span></span>
<span data-ttu-id="18385-651">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-651">Disabled</span></span>|<span data-ttu-id="18385-652">hello 원본 서버 오류 toohello 요청자에 게를 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-652">hello origin server's error will be forwarded toohello requester.</span></span>

<span data-ttu-id="18385-653">**기본 동작:** 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-653">**Default Behavior:** Disabled</span></span>

###<a name="stale-while-revalidate"></a><span data-ttu-id="18385-654">유효성 재검사 중 기한 경과</span><span class="sxs-lookup"><span data-stu-id="18385-654">Stale While Revalidate</span></span>
<span data-ttu-id="18385-655">**목적:** edge 서버 tooserve 부실 콘텐츠 toohello 요청자 유효성 재검사 수행 하는 동안 허용 하 여 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-655">**Purpose:** Improves performance by allowing our edge servers tooserve stale content toohello requester while revalidation takes place.</span></span>

<span data-ttu-id="18385-656">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-656">Key information:</span></span>

- <span data-ttu-id="18385-657">이 기능의 hello 동작 toohello 선택한 시간 단위에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="18385-657">hello behavior of this feature varies according toohello selected time unit.</span></span>
    - <span data-ttu-id="18385-658">**시간 단위:** 시간의 길이 지정 하 고 시간 단위 (예: 초, 분, 시간 등) tooallow 부실 콘텐츠 배달을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-658">**Time Unit:** Specify a length of time and select a time unit (e.g., Seconds, Minutes, Hours, etc.) tooallow stale content delivery.</span></span> <span data-ttu-id="18385-659">이 유형의 설치 프로그램을 허용 배달할 수 있는 시간의 hello CDN tooextend hello 길이 콘텐츠 다음 수식을 toohello에 따라 유효성 검사를 요구 하기 전에:**TTL** + **부실 하는 동안 유효성을 다시 검사 시간**</span><span class="sxs-lookup"><span data-stu-id="18385-659">This type of setup allows hello CDN tooextend hello length of time that it may deliver content before requiring validation according toohello following formula:**TTL** + **Stale While Revalidate Time**</span></span> 
    - <span data-ttu-id="18385-660">**Off:** 불완전 한 콘텐츠 구현 될 수 있습니다에 대 한 "Off" 요청 하기 전에 toorequire 유효성 재검사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-660">**Off:** Select "Off" toorequire revalidation before a request for stale content may be served.</span></span>
        - <span data-ttu-id="18385-661">기간은 적용할 수 없으므로 지정하지 않아야 하며, 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-661">Do not specify a length of time since it is inapplicable and will be ignored.</span></span>

<span data-ttu-id="18385-662">**기본 동작:** 끄기</span><span class="sxs-lookup"><span data-stu-id="18385-662">**Default Behavior:** Off.</span></span> <span data-ttu-id="18385-663">유효성 재검사 hello 콘텐츠 제공 될 수 있지만 요청 하기 전에 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-663">Revalidation must take place before hello requested content can be served.</span></span>

###<a name="comment"></a><span data-ttu-id="18385-664">주석</span><span class="sxs-lookup"><span data-stu-id="18385-664">Comment</span></span>
<span data-ttu-id="18385-665">**목적:** 규칙 내에서 추가 참고 toobe 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-665">**Purpose:** Allows a note toobe added within a rule.</span></span>

<span data-ttu-id="18385-666">규칙의 일반적인 용도로 hello tooprovide 추가 정보는 하는이 기능에 대 한 사용 되었거나, 특정 조건 또는 기능을 일치 하는 이유 toohello 규칙 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-666">One use for this feature is tooprovide additional information on hello general purpose of a rule or why a particular match condition or feature was added toohello rule.</span></span>

<span data-ttu-id="18385-667">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-667">Key information:</span></span>

- <span data-ttu-id="18385-668">최대 150자를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-668">A maximum of 150 characters may be specified.</span></span>
- <span data-ttu-id="18385-669">영숫자를 사용 하는지 tooonly를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-669">Make sure tooonly use alphanumeric characters.</span></span>
- <span data-ttu-id="18385-670">이 기능은 hello 규칙의 hello 동작에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-670">This feature does not affect hello behavior of hello rule.</span></span> <span data-ttu-id="18385-671">단순히 말로 tooprovide 또는 나중에 참조할 수에 대 한 정보를 제공할 수 있는 영역 hello 규칙 문제를 해결할 때 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-671">It is merely meant tooprovide an area where you can provide information for future reference or that may help when troubleshooting hello rule.</span></span>
 
## <a name="headers"></a><span data-ttu-id="18385-672">헤더</span><span class="sxs-lookup"><span data-stu-id="18385-672">Headers</span></span>

<span data-ttu-id="18385-673">이러한 기능을 디자인 된 tooadd, 수정 또는 hello 요청 또는 응답에서 헤더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-673">These features are designed tooadd, modify, or delete headers from hello request or response.</span></span>

<span data-ttu-id="18385-674">이름</span><span class="sxs-lookup"><span data-stu-id="18385-674">Name</span></span> | <span data-ttu-id="18385-675">목적</span><span class="sxs-lookup"><span data-stu-id="18385-675">Purpose</span></span>
-----|--------
<span data-ttu-id="18385-676">Age 응답 헤더</span><span class="sxs-lookup"><span data-stu-id="18385-676">Age Response Header</span></span> | <span data-ttu-id="18385-677">Age 응답 헤더 toohello 요청자에 게 전송 하는 hello 응답에 포함될지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-677">Determines whether an Age response header will be included in hello response sent toohello requester.</span></span>
<span data-ttu-id="18385-678">디버그 캐시 응답 헤더</span><span class="sxs-lookup"><span data-stu-id="18385-678">Debug Cache Response Headers</span></span> | <span data-ttu-id="18385-679">응답 hello 요청 된 자산에 대 한 캐시 정책을 hello에 정보를 제공 하는 hello EC-X-debug 응답 헤더에 포함 될 수 있습니다 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-679">Determines whether a response may include hello X-EC-Debug response header which provides information on hello cache policy for hello requested asset.</span></span>
<span data-ttu-id="18385-680">클라이언트 요청 헤더 수정</span><span class="sxs-lookup"><span data-stu-id="18385-680">Modify Client Request Header</span></span> | <span data-ttu-id="18385-681">요청에서 헤더를 덮어쓰기, 추가 또는 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-681">Overwrites, appends, or deletes a header from a request.</span></span>
<span data-ttu-id="18385-682">클라이언트 응답 헤더 수정</span><span class="sxs-lookup"><span data-stu-id="18385-682">Modify Client Response Header</span></span> | <span data-ttu-id="18385-683">응답에서 헤더를 덮어쓰기, 추가 또는 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-683">Overwrites, appends, or deletes a header from a response.</span></span>
<span data-ttu-id="18385-684">클라이언트 IP 사용자 지정 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="18385-684">Set Client IP Custom Header</span></span> | <span data-ttu-id="18385-685">사용자 지정 요청 헤더로 hello 요청 클라이언트의 IP 주소 hello toobe 추가 toohello 요청을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-685">Allows hello IP address of hello requesting client toobe added toohello request as a custom request header.</span></span>

###<a name="age-response-header"></a><span data-ttu-id="18385-686">Age 응답 헤더</span><span class="sxs-lookup"><span data-stu-id="18385-686">Age Response Header</span></span>
<span data-ttu-id="18385-687">**용도**: Age 응답 헤더를 보낸 응답 toohello 요청자 hello에에서 포함될지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-687">**Purpose**: Determines whether an Age response header will be included in hello response sent toohello requester.</span></span>
<span data-ttu-id="18385-688">값</span><span class="sxs-lookup"><span data-stu-id="18385-688">Value</span></span>|<span data-ttu-id="18385-689">결과</span><span class="sxs-lookup"><span data-stu-id="18385-689">Result</span></span>
--|--
<span data-ttu-id="18385-690">사용</span><span class="sxs-lookup"><span data-stu-id="18385-690">Enabled</span></span> | <span data-ttu-id="18385-691">hello Age 응답 헤더 toohello 요청자에 게 전송 하는 hello 응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-691">hello Age response header will be included in hello response sent toohello requester.</span></span>
<span data-ttu-id="18385-692">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-692">Disabled</span></span> | <span data-ttu-id="18385-693">hello Age 응답 헤더 toohello 요청자에 게 전송 하는 hello 응답에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-693">hello Age response header will be excluded from hello response sent toohello requester.</span></span>

<span data-ttu-id="18385-694">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-694">**Default Behavior**: Disabled.</span></span>

###<a name="debug-cache-response-headers"></a><span data-ttu-id="18385-695">디버그 캐시 응답 헤더</span><span class="sxs-lookup"><span data-stu-id="18385-695">Debug Cache Response Headers</span></span>
<span data-ttu-id="18385-696">**목적:** 응답 hello 요청 된 자산에 대 한 캐시 정책을 hello에 정보를 제공 하는 X-EC-디버그 응답 헤더에 포함 될 수 있습니다 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-696">**Purpose:** Determines whether a response may include the X-EC-Debug response header which provides information on hello cache policy for hello requested asset.</span></span>

<span data-ttu-id="18385-697">디버그에서 캐시 응답 헤더 모두 hello 다음에 해당할 때 hello 응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-697">Debug cache response headers will be included in hello response when both of hello following are true:</span></span>

- <span data-ttu-id="18385-698">hello 원하는 요청에서 hello 디버그 캐시 응답 헤더 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-698">hello Debug Cache Response Headers Feature has been enabled on hello desired request.</span></span>
- <span data-ttu-id="18385-699">요청 위에 hello hello 응답에 포함 되어야 디버그 캐시 응답 헤더의 hello 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-699">hello above request defines hello set of debug cache response headers that will be included in hello response.</span></span>

<span data-ttu-id="18385-700">캐시 응답 헤더를 헤더 뒤에 오는 hello를 포함 하 여 요청할 수 있습니다 및 hello 요청에서 원하는 지시문 hello 디버그:</span><span class="sxs-lookup"><span data-stu-id="18385-700">Debug cache response headers may be requested by including hello following header and hello desired directives in hello request:</span></span>

<span data-ttu-id="18385-701">X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_</span><span class="sxs-lookup"><span data-stu-id="18385-701">X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_</span></span>

<span data-ttu-id="18385-702">**예제:**</span><span class="sxs-lookup"><span data-stu-id="18385-702">**Example:**</span></span>

<span data-ttu-id="18385-703">X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state</span><span class="sxs-lookup"><span data-stu-id="18385-703">X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state</span></span>

<span data-ttu-id="18385-704">값</span><span class="sxs-lookup"><span data-stu-id="18385-704">Value</span></span>|<span data-ttu-id="18385-705">결과</span><span class="sxs-lookup"><span data-stu-id="18385-705">Result</span></span>
-|-
<span data-ttu-id="18385-706">사용</span><span class="sxs-lookup"><span data-stu-id="18385-706">Enabled</span></span>|<span data-ttu-id="18385-707">디버그 캐시 응답 헤더에 대한 요청에서 X-EC-Debug 헤더를 포함한 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-707">Requests for debug cache response headers will return a response that includes the X-EC-Debug header.</span></span>
<span data-ttu-id="18385-708">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-708">Disabled</span></span>|<span data-ttu-id="18385-709">X-EC-디버그 응답 헤더는 hello 응답에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-709">The X-EC-Debug response header will be excluded from hello response.</span></span>

<span data-ttu-id="18385-710">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-710">**Default Behavior:** Disabled.</span></span>

###<a name="modify-client-response-header"></a><span data-ttu-id="18385-711">클라이언트 응답 헤더 수정</span><span class="sxs-lookup"><span data-stu-id="18385-711">Modify Client Response Header</span></span>
<span data-ttu-id="18385-712">**목적:** 각 요청에는 이를 설명하는 [요청 헤더]() 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-712">**Purpose:** Each request contains a set of [request headers]() that describe it.</span></span> <span data-ttu-id="18385-713">이 기능은 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-713">This feature can either:</span></span>

- <span data-ttu-id="18385-714">뒤에 추가 또는 tooa 요청 헤더를 할당 하는 hello 값을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="18385-714">Append or overwrite hello value assigned tooa request header.</span></span> <span data-ttu-id="18385-715">지정 된 요청 헤더 hello가 없는 경우 다음이 기능은 추가 됩니다 toohello 요청.</span><span class="sxs-lookup"><span data-stu-id="18385-715">If hello specified request header does not exist, then this feature will add it toohello request.</span></span>
- <span data-ttu-id="18385-716">Hello 요청에서 요청 헤더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-716">Delete a request header from hello request.</span></span>

<span data-ttu-id="18385-717">Tooan 원본 서버에 전달 된 요청에는이 기능을 통해 변경 하는 hello 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-717">Requests that are forwarded tooan origin server will reflect hello changes made by this feature.</span></span>

<span data-ttu-id="18385-718">요청 헤더에 hello 다음 동작 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-718">One of hello following actions can be performed on a request header:</span></span>

<span data-ttu-id="18385-719">옵션</span><span class="sxs-lookup"><span data-stu-id="18385-719">Option</span></span>|<span data-ttu-id="18385-720">설명</span><span class="sxs-lookup"><span data-stu-id="18385-720">Description</span></span>|<span data-ttu-id="18385-721">예</span><span class="sxs-lookup"><span data-stu-id="18385-721">Example</span></span>
-|-|-
<span data-ttu-id="18385-722">추가</span><span class="sxs-lookup"><span data-stu-id="18385-722">Append</span></span>|<span data-ttu-id="18385-723">hello는 toend hello 기존 요청 헤더 값의 값이 추가 되 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-723">hello specified value will be added toend of hello existing request header value.</span></span>|<span data-ttu-id="18385-724">**요청 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="18385-724">**Request header value (Client):**Value1</span></span> <br/> <span data-ttu-id="18385-725">**요청 헤더 값(HTTP 규칙 엔진):** Value2</span><span class="sxs-lookup"><span data-stu-id="18385-725">**Request header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="18385-726">**새 요청 헤더 값:** Value1Value2</span><span class="sxs-lookup"><span data-stu-id="18385-726">**New request header value:** Value1Value2</span></span>
<span data-ttu-id="18385-727">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-727">Overwrite</span></span>|<span data-ttu-id="18385-728">값을 지정 하는 hello 요청 헤더 값 집합 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-728">hello request header value will be set toohello specified value.</span></span>|<span data-ttu-id="18385-729">**요청 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="18385-729">**Request header value (Client):**Value1</span></span> <br/><span data-ttu-id="18385-730">**요청 헤더 값(HTTP 규칙 엔진):** Value2</span><span class="sxs-lookup"><span data-stu-id="18385-730">**Request header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="18385-731">**새 요청 헤더 값:** Value2</span><span class="sxs-lookup"><span data-stu-id="18385-731">**New request header value:** Value2</span></span> <br/>
<span data-ttu-id="18385-732">삭제</span><span class="sxs-lookup"><span data-stu-id="18385-732">Delete</span></span>|<span data-ttu-id="18385-733">Hello 지정 된 요청 헤더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-733">Deletes hello specified request header.</span></span>|<span data-ttu-id="18385-734">**요청 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="18385-734">**Request header value (Client):**Value1</span></span> <br/> <span data-ttu-id="18385-735">**클라이언트 요청 헤더 구성 수정:** Delete hello 요청 헤더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-735">**Modify Client Request Header configuration:** Delete hello request header in question.</span></span> <br/><span data-ttu-id="18385-736">**결과:** hello를 지정 된 요청 헤더 toohello 원본 서버에 전달 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-736">**Result:** hello specified request header will not be forwarded toohello origin server.</span></span>

<span data-ttu-id="18385-737">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-737">Key information:</span></span>

- <span data-ttu-id="18385-738">Name 옵션에 지정 된 hello 값 hello 원하는 요청 헤더에 대 한 정확 하 게 일치 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-738">Make sure that hello value specified in the Name option is an exact match for hello desired request header.</span></span>
- <span data-ttu-id="18385-739">대/소문자가 헤더를 식별 하는 데 hello 목적을 위해 계정에 작성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-739">Case is not taken into account for hello purpose of identifying a header.</span></span> <span data-ttu-id="18385-740">예를 들어 모든 변형 된 캐시 제어 헤더 이름 다음 hello 사용된 tooidentify를 지정할 수 있으며 해당:</span><span class="sxs-lookup"><span data-stu-id="18385-740">For example, any of hello following variations of the Cache-Control header name can be used tooidentify it:</span></span>
    - <span data-ttu-id="18385-741">cache-control</span><span class="sxs-lookup"><span data-stu-id="18385-741">cache-control</span></span>
    - <span data-ttu-id="18385-742">CACHE-CONTROL</span><span class="sxs-lookup"><span data-stu-id="18385-742">CACHE-CONTROL</span></span>
    - <span data-ttu-id="18385-743">cachE-Control</span><span class="sxs-lookup"><span data-stu-id="18385-743">cachE-Control</span></span>
- <span data-ttu-id="18385-744">있는지 tooonly 헤더 이름을 지정할 때 영숫자 문자, 대시 또는 밑줄만 사용 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-744">Make sure tooonly use alphanumeric characters, dashes, or underscores when specifying a header name.</span></span>
- <span data-ttu-id="18385-745">헤더는 삭제를 tooan 원본 서버는에 지 서버에서 전달 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-745">Deleting a header will prevent it from being forwarded tooan origin server by our edge servers.</span></span>
- <span data-ttu-id="18385-746">hello 다음 헤더 예약 되어 있으므로이 기능을 통해 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-746">hello following headers are reserved and cannot be modified by this feature:</span></span>
    - <span data-ttu-id="18385-747">forwarded</span><span class="sxs-lookup"><span data-stu-id="18385-747">forwarded</span></span>
    - <span data-ttu-id="18385-748">host</span><span class="sxs-lookup"><span data-stu-id="18385-748">host</span></span>
    - <span data-ttu-id="18385-749">via</span><span class="sxs-lookup"><span data-stu-id="18385-749">via</span></span>
    - <span data-ttu-id="18385-750">Warning</span><span class="sxs-lookup"><span data-stu-id="18385-750">warning</span></span>
    - <span data-ttu-id="18385-751">x-forwarded-for</span><span class="sxs-lookup"><span data-stu-id="18385-751">x-forwarded-for</span></span>
    - <span data-ttu-id="18385-752">"x-ec"로 시작하는 모든 헤더 이름은 예약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-752">All header names that start with "x-ec" are reserved.</span></span>

###<a name="modify-client-response-header"></a><span data-ttu-id="18385-753">클라이언트 응답 헤더 수정</span><span class="sxs-lookup"><span data-stu-id="18385-753">Modify Client Response Header</span></span>
<span data-ttu-id="18385-754">각 응답에는 이를 설명하는 [응답 헤더]() 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-754">Each response contains a set of [response headers]() that describe it.</span></span> <span data-ttu-id="18385-755">이 기능은 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-755">This feature can either:</span></span>

- <span data-ttu-id="18385-756">뒤에 추가 또는 tooa 응답 헤더를 할당 하는 hello 값을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="18385-756">Append or overwrite hello value assigned tooa response header.</span></span> <span data-ttu-id="18385-757">Hello 지정 된 요청 헤더가 없는 경우 다음이 기능은 됩니다 추가 toohello 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-757">If hello specified request header does not exist, then this feature will add it toohello response.</span></span>
- <span data-ttu-id="18385-758">Hello 응답에서 응답 헤더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-758">Delete a response header from hello response.</span></span>

<span data-ttu-id="18385-759">기본적으로 응답 헤더 값은 원본 서버 및 에지 서버에서 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-759">By default, response header values are defined by an origin server and by our edge servers.</span></span>

<span data-ttu-id="18385-760">응답 헤더에서 동작을 수행 하는 hello 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-760">One of hello following actions can be performed on a response header:</span></span>

<span data-ttu-id="18385-761">옵션</span><span class="sxs-lookup"><span data-stu-id="18385-761">Option</span></span>|<span data-ttu-id="18385-762">설명</span><span class="sxs-lookup"><span data-stu-id="18385-762">Description</span></span>|<span data-ttu-id="18385-763">예</span><span class="sxs-lookup"><span data-stu-id="18385-763">Example</span></span>
-|-|-
<span data-ttu-id="18385-764">추가</span><span class="sxs-lookup"><span data-stu-id="18385-764">Append</span></span>|<span data-ttu-id="18385-765">hello는 toend hello 기존 요청 헤더 값의 값이 추가 되 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-765">hello specified value will be added toend of hello existing request header value.</span></span>|<span data-ttu-id="18385-766">**응답 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="18385-766">**Response header value (Client):**Value1</span></span> <br/> <span data-ttu-id="18385-767">**응답 헤더 값(HTTP 규칙 엔진):** Value2</span><span class="sxs-lookup"><span data-stu-id="18385-767">**Response header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="18385-768">**새 응답 헤더 값:** Value1Value2</span><span class="sxs-lookup"><span data-stu-id="18385-768">**New Response header value:** Value1Value2</span></span>
<span data-ttu-id="18385-769">덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-769">Overwrite</span></span>|<span data-ttu-id="18385-770">값을 지정 하는 hello 요청 헤더 값 집합 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-770">hello request header value will be set toohello specified value.</span></span>|<span data-ttu-id="18385-771">**응답 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="18385-771">**Response header value (Client):**Value1</span></span> <br/><span data-ttu-id="18385-772">**응답 헤더 값(HTTP 규칙 엔진):** Value2</span><span class="sxs-lookup"><span data-stu-id="18385-772">**Response header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="18385-773">**새 응답 헤더 값:** Value2</span><span class="sxs-lookup"><span data-stu-id="18385-773">**New response header value:** Value2</span></span> <br/>
<span data-ttu-id="18385-774">삭제</span><span class="sxs-lookup"><span data-stu-id="18385-774">Delete</span></span>|<span data-ttu-id="18385-775">Hello 지정 된 요청 헤더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-775">Deletes hello specified request header.</span></span>|<span data-ttu-id="18385-776">**요청 헤더 값(클라이언트):** Value1</span><span class="sxs-lookup"><span data-stu-id="18385-776">**Request header value (Client):** Value1</span></span> <br/> <span data-ttu-id="18385-777">**클라이언트 요청 헤더 구성 수정:** Delete hello 응답 헤더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-777">**Modify Client Request Header configuration:** Delete hello response header in question.</span></span> <br/><span data-ttu-id="18385-778">**결과:** hello를 지정 된 응답 헤더 toohello 요청자에 게 전달 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-778">**Result:** hello specified response header will not be forwarded toohello requester.</span></span>

<span data-ttu-id="18385-779">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-779">Key information:</span></span>

- <span data-ttu-id="18385-780">Name 옵션에 지정 된 hello 값 hello 원하는 응답 헤더에 대 한 정확 하 게 일치 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-780">Make sure that hello value specified in the Name option is an exact match for hello desired response header.</span></span> 
- <span data-ttu-id="18385-781">대/소문자가 헤더를 식별 하는 데 hello 목적을 위해 계정에 작성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-781">Case is not taken into account for hello purpose of identifying a header.</span></span> <span data-ttu-id="18385-782">예를 들어 모든 변형 된 캐시 제어 헤더 이름 다음 hello 사용된 tooidentify를 지정할 수 있으며 해당:</span><span class="sxs-lookup"><span data-stu-id="18385-782">For example, any of hello following variations of the Cache-Control header name can be used tooidentify it:</span></span>
    - <span data-ttu-id="18385-783">cache-control</span><span class="sxs-lookup"><span data-stu-id="18385-783">cache-control</span></span>
    - <span data-ttu-id="18385-784">CACHE-CONTROL</span><span class="sxs-lookup"><span data-stu-id="18385-784">CACHE-CONTROL</span></span>
    - <span data-ttu-id="18385-785">cachE-Control</span><span class="sxs-lookup"><span data-stu-id="18385-785">cachE-Control</span></span>
- <span data-ttu-id="18385-786">헤더는 삭제를 toohello 요청자에 게 전달 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-786">Deleting a header will prevent it from being forwarded toohello requester.</span></span>
- <span data-ttu-id="18385-787">hello 다음 헤더 예약 되어 있으므로이 기능을 통해 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-787">hello following headers are reserved and cannot be modified by this feature:</span></span>
    - <span data-ttu-id="18385-788">accept-encoding</span><span class="sxs-lookup"><span data-stu-id="18385-788">accept-encoding</span></span>
    - <span data-ttu-id="18385-789">age</span><span class="sxs-lookup"><span data-stu-id="18385-789">age</span></span>
    - <span data-ttu-id="18385-790">connection</span><span class="sxs-lookup"><span data-stu-id="18385-790">connection</span></span>
    - <span data-ttu-id="18385-791">content-encoding</span><span class="sxs-lookup"><span data-stu-id="18385-791">content-encoding</span></span>
    - <span data-ttu-id="18385-792">content-length</span><span class="sxs-lookup"><span data-stu-id="18385-792">content-length</span></span>
    - <span data-ttu-id="18385-793">content-range</span><span class="sxs-lookup"><span data-stu-id="18385-793">content-range</span></span>
    - <span data-ttu-id="18385-794">date</span><span class="sxs-lookup"><span data-stu-id="18385-794">date</span></span>
    - <span data-ttu-id="18385-795">server</span><span class="sxs-lookup"><span data-stu-id="18385-795">server</span></span>
    - <span data-ttu-id="18385-796">trailer</span><span class="sxs-lookup"><span data-stu-id="18385-796">trailer</span></span>
    - <span data-ttu-id="18385-797">transfer-encoding</span><span class="sxs-lookup"><span data-stu-id="18385-797">transfer-encoding</span></span>
    - <span data-ttu-id="18385-798">업그레이드</span><span class="sxs-lookup"><span data-stu-id="18385-798">upgrade</span></span>
    - <span data-ttu-id="18385-799">vary</span><span class="sxs-lookup"><span data-stu-id="18385-799">vary</span></span>
    - <span data-ttu-id="18385-800">via</span><span class="sxs-lookup"><span data-stu-id="18385-800">via</span></span>
    - <span data-ttu-id="18385-801">Warning</span><span class="sxs-lookup"><span data-stu-id="18385-801">warning</span></span>
    - <span data-ttu-id="18385-802">"x-ec"로 시작하는 모든 헤더 이름은 예약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-802">All header names that start with "x-ec" are reserved.</span></span>

###<a name="set-client-ip-custom-header"></a><span data-ttu-id="18385-803">클라이언트 IP 사용자 지정 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="18385-803">Set Client IP Custom Header</span></span>
<span data-ttu-id="18385-804">**목적:** IP 주소 toohello 요청 하 여 hello 요청 하는 클라이언트를 식별 하는 사용자 지정 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-804">**Purpose:** Adds a custom header that identifies hello requesting client by IP address toohello request.</span></span>

<span data-ttu-id="18385-805">헤더 이름 옵션에는 hello 클라이언트의 IP 주소를 저장할 hello 사용자 지정 요청 헤더의 hello 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-805">The Header name option defines hello name of hello custom request header where hello client's IP address will be stored.</span></span>

<span data-ttu-id="18385-806">이 기능을 사용 하는 고객 원본 서버 toofind 클라이언트 IP 주소는 사용자 지정 요청 헤더를 통해 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-806">This feature allows a customer origin server toofind out client IP addresses through a custom request header.</span></span> <span data-ttu-id="18385-807">Hello 요청을 캐시에서 서비스 하는 경우 원본 서버 hello hello 클라이언트의 IP 주소의 알림을 받지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-807">If hello request is served from cache, then hello origin server will not be informed of hello client's IP address.</span></span> <span data-ttu-id="18385-808">따라서 이 기능은 캐시되지 않는 ADN 또는 자산과 함께 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-808">Therefore, it is recommended that this feature be used with ADN or assets that will not be cached.</span></span>

<span data-ttu-id="18385-809">해당 hello 지정 된 헤더 이름이 hello 다음 중 하나라도 일치 하지 않습니다 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="18385-809">Please make sure that hello specified header name does not match any of hello following:</span></span>

- <span data-ttu-id="18385-810">표준 요청 헤더 이름 -</span><span class="sxs-lookup"><span data-stu-id="18385-810">Standard request header names.</span></span> <span data-ttu-id="18385-811">표준 헤더 이름 목록은 [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-811">A list of standard header names can be found in [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).</span></span>
- <span data-ttu-id="18385-812">예약된 헤더 이름</span><span class="sxs-lookup"><span data-stu-id="18385-812">Reserved header names:</span></span>
    - <span data-ttu-id="18385-813">forwarded-for</span><span class="sxs-lookup"><span data-stu-id="18385-813">forwarded-for</span></span>
    - <span data-ttu-id="18385-814">host</span><span class="sxs-lookup"><span data-stu-id="18385-814">host</span></span>
    - <span data-ttu-id="18385-815">vary</span><span class="sxs-lookup"><span data-stu-id="18385-815">vary</span></span>
    - <span data-ttu-id="18385-816">via</span><span class="sxs-lookup"><span data-stu-id="18385-816">via</span></span>
    - <span data-ttu-id="18385-817">Warning</span><span class="sxs-lookup"><span data-stu-id="18385-817">warning</span></span>
    - <span data-ttu-id="18385-818">x-forwarded-for</span><span class="sxs-lookup"><span data-stu-id="18385-818">x-forwarded-for</span></span>
    - <span data-ttu-id="18385-819">"x-ec"로 시작하는 모든 헤더 이름은 예약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-819">All header names that start with "x-ec" are reserved.</span></span>
 
## <a name="logs"></a><span data-ttu-id="18385-820">로그</span><span class="sxs-lookup"><span data-stu-id="18385-820">Logs</span></span>

<span data-ttu-id="18385-821">이러한 기능은 원시 로그 파일에 저장 된 디자인 된 toocustomize hello 데이터에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-821">These features are designed toocustomize hello data stored in raw log files.</span></span>

<span data-ttu-id="18385-822">이름</span><span class="sxs-lookup"><span data-stu-id="18385-822">Name</span></span> | <span data-ttu-id="18385-823">목적</span><span class="sxs-lookup"><span data-stu-id="18385-823">Purpose</span></span>
-----|--------
<span data-ttu-id="18385-824">사용자 지정 로그 필드 1</span><span class="sxs-lookup"><span data-stu-id="18385-824">Custom Log Field 1</span></span> | <span data-ttu-id="18385-825">Hello 형식과 원시 로그 파일의 사용자 지정 로그 필드 toohello 할당할 수 있는 hello 내용을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-825">Determines hello format and hello content that will be assigned toohello custom log field in a raw log file.</span></span>
<span data-ttu-id="18385-826">로그 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="18385-826">Log Query String</span></span> | <span data-ttu-id="18385-827">쿼리 문자열 hello URL 액세스 로그에 함께 저장 하는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-827">Determines whether a query string will be stored along with hello URL in access logs.</span></span>

###<a name="custom-log-field-1"></a><span data-ttu-id="18385-828">사용자 지정 로그 필드 1</span><span class="sxs-lookup"><span data-stu-id="18385-828">Custom Log Field 1</span></span>
<span data-ttu-id="18385-829">**목적:** hello 형식과 원시 로그 파일의 사용자 지정 로그 필드 toohello 할당할 수 있는 hello 내용을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-829">**Purpose:** Determines hello format and hello content that will be assigned toohello custom log field in a raw log file.</span></span>

<span data-ttu-id="18385-830">이 사용자 정의 필드 뒤에 있는 주요 목적은 hello는 tooallow toodetermine 요청 및 응답 헤더 값을 로그 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-830">hello main purpose behind this custom field is tooallow you toodetermine which request and response header values will be stored in your log files.</span></span>

<span data-ttu-id="18385-831">기본적으로 사용자 지정 로그 필드 hello 라고 "x-ec_custom-1".</span><span class="sxs-lookup"><span data-stu-id="18385-831">By default, hello custom log field is called "x-ec_custom-1."</span></span> <span data-ttu-id="18385-832">그러나이 필드의 hello 이름을 사용자 지정할 수에서 [원시 로그 설정 페이지]()합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-832">However, hello name of this field can be customized from the [Raw Log Settings page]().</span></span>

<span data-ttu-id="18385-833">hello toospecify 요청 및 응답 헤더를 사용 해야 하는 서식 지정 아래 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-833">hello formatting that you should use toospecify request and response headers is defined below.</span></span>

<span data-ttu-id="18385-834">헤더 형식</span><span class="sxs-lookup"><span data-stu-id="18385-834">Header Type</span></span>|<span data-ttu-id="18385-835">형식</span><span class="sxs-lookup"><span data-stu-id="18385-835">Format</span></span>|<span data-ttu-id="18385-836">예</span><span class="sxs-lookup"><span data-stu-id="18385-836">Examples</span></span>
-|-|-
<span data-ttu-id="18385-837">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="18385-837">Request Header</span></span>|<span data-ttu-id="18385-838">%{[RequestHeader]()}[i]()</span><span class="sxs-lookup"><span data-stu-id="18385-838">%{[RequestHeader]()}[i]()</span></span> | <span data-ttu-id="18385-839">%{Accept-Encoding}i</span><span class="sxs-lookup"><span data-stu-id="18385-839">%{Accept-Encoding}i</span></span> <br/> <span data-ttu-id="18385-840">{Referer}i</span><span class="sxs-lookup"><span data-stu-id="18385-840">{Referer}i</span></span> <br/> <span data-ttu-id="18385-841">%{Authorization}i</span><span class="sxs-lookup"><span data-stu-id="18385-841">%{Authorization}i</span></span>
<span data-ttu-id="18385-842">응답 헤더</span><span class="sxs-lookup"><span data-stu-id="18385-842">Response Header</span></span>|<span data-ttu-id="18385-843">%{[ResponseHeader]()}[o]()</span><span class="sxs-lookup"><span data-stu-id="18385-843">%{[ResponseHeader]()}[o]()</span></span>| <span data-ttu-id="18385-844">%{Age}o</span><span class="sxs-lookup"><span data-stu-id="18385-844">%{Age}o</span></span> <br/> <span data-ttu-id="18385-845">%{Content-Type}o</span><span class="sxs-lookup"><span data-stu-id="18385-845">%{Content-Type}o</span></span> <br/> <span data-ttu-id="18385-846">%{Cookie}o</span><span class="sxs-lookup"><span data-stu-id="18385-846">%{Cookie}o</span></span>

<span data-ttu-id="18385-847">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-847">Key information:</span></span>

- <span data-ttu-id="18385-848">사용자 지정 로그 필드는 헤더 필드와 일반 텍스트의 조합을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-848">A custom log field can contain any combination of header fields and plain text.</span></span>
- <span data-ttu-id="18385-849">이 필드에 유효한 문자는 hello 다음: 영숫자 (즉, 0-9, a-z 및 A-z), 콜론, 세미콜론, 아포스트로피, 쉼표, 마침표, 밑줄, 등호, 괄호, 대괄호, 대시와 공백의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-849">Valid characters for this field include hello following: alphanumeric (i.e., 0-9, a-z, and A-Z), dashes, colons, semi-colons, apostrophes, commas, periods, underscores, equal signs, parentheses, brackets, and spaces.</span></span> <span data-ttu-id="18385-850">hello 백분율 기호와 중괄호만 허용 됩니다 때 toospecify 헤더 필드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-850">hello percentage symbol and curly braces are only allowed when used toospecify a header field.</span></span>
- <span data-ttu-id="18385-851">각 지정 된 헤더 필드에 대 한 hello 맞춤법 hello 원하는 요청/응답 헤더 이름이 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-851">hello spelling for each specified header field must match hello desired request/response header name.</span></span>
- <span data-ttu-id="18385-852">Toospecify 원하는 경우 여러 헤더 이면 것이 좋습니다를 사용 하는 구분 기호 tooindicate 각 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-852">If you would like toospecify multiple headers, then it is recommended that you use a separator tooindicate each header.</span></span> <span data-ttu-id="18385-853">예를 들어 각 헤더에 약어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-853">For example, you could use an abbreviation for each header.</span></span> <span data-ttu-id="18385-854">샘플 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-854">Sample syntax is provided below.</span></span>
    - <span data-ttu-id="18385-855">AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o</span><span class="sxs-lookup"><span data-stu-id="18385-855">AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o</span></span> 

<span data-ttu-id="18385-856">**기본값:** -</span><span class="sxs-lookup"><span data-stu-id="18385-856">**Default Value:** -</span></span>

###<a name="log-query-string"></a><span data-ttu-id="18385-857">로그 쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="18385-857">Log Query String</span></span>
<span data-ttu-id="18385-858">**목적:** 쿼리 문자열 hello URL 액세스 로그에 함께 저장 하는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-858">**Purpose:** Determines whether a query string will be stored along with hello URL in access logs.</span></span>

<span data-ttu-id="18385-859">값</span><span class="sxs-lookup"><span data-stu-id="18385-859">Value</span></span>|<span data-ttu-id="18385-860">결과</span><span class="sxs-lookup"><span data-stu-id="18385-860">Result</span></span>
-|-
<span data-ttu-id="18385-861">사용</span><span class="sxs-lookup"><span data-stu-id="18385-861">Enabled</span></span>|<span data-ttu-id="18385-862">Url 액세스 로그에 기록할 때 쿼리 문자열의 hello 저장소를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-862">Allows hello storage of query strings when recording URLs in an access log.</span></span> <span data-ttu-id="18385-863">URL에 쿼리 문자열이 없으면 이 옵션이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-863">If a URL does not contain a query string, then this option will not have an effect.</span></span>
<span data-ttu-id="18385-864">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-864">Disabled</span></span>|<span data-ttu-id="18385-865">Hello 기본 동작을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-865">Restores hello default behavior.</span></span> <span data-ttu-id="18385-866">hello 기본 동작은 Url 액세스 로그에 기록할 때 tooignore 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-866">hello default behavior is tooignore query strings when recording URLs in an access log.</span></span>

<span data-ttu-id="18385-867">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-867">**Default Behavior:** Disabled.</span></span>

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a><span data-ttu-id="18385-868">원본</span><span class="sxs-lookup"><span data-stu-id="18385-868">Origin</span></span>

<span data-ttu-id="18385-869">이러한 기능은 디자인 된 toocontrol hello CDN 원본 서버와 통신 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-869">These features are designed toocontrol how hello CDN communicates with an origin server.</span></span>

<span data-ttu-id="18385-870">이름</span><span class="sxs-lookup"><span data-stu-id="18385-870">Name</span></span> | <span data-ttu-id="18385-871">목적</span><span class="sxs-lookup"><span data-stu-id="18385-871">Purpose</span></span>
-----|--------
<span data-ttu-id="18385-872">최대 연결 유지 요청</span><span class="sxs-lookup"><span data-stu-id="18385-872">Maximum Keep-Alive Requests</span></span> | <span data-ttu-id="18385-873">닫 혔 기 전에 hello 유지 연결에 대 한 요청의 최대 수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-873">Defines hello maximum number of requests for a Keep-Alive connection before it is closed.</span></span>
<span data-ttu-id="18385-874">프록시 특별 헤더</span><span class="sxs-lookup"><span data-stu-id="18385-874">Proxy Special Headers</span></span> | <span data-ttu-id="18385-875">Hello에 지 서버 tooan 원본 서버에서 전달 하는 CDN에 관련 된 요청 헤더 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-875">Defines hello set of CDN-specific request headers that will be forwarded from an edge server tooan origin server.</span></span>


###<a name="maximum-keep-alive-requests"></a><span data-ttu-id="18385-876">최대 연결 유지 요청</span><span class="sxs-lookup"><span data-stu-id="18385-876">Maximum Keep-Alive Requests</span></span>
<span data-ttu-id="18385-877">**목적:** 연결이 닫히기 전에 hello 유지 연결에 대 한 요청의 최대 수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-877">**Purpose:** Defines hello maximum number of requests for a Keep-Alive connection before it is closed.</span></span>

<span data-ttu-id="18385-878">Hello 요청 tooa 낮은 값의 최대 수를 설정 하는 것이 좋습니다 및 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-878">Setting hello maximum number of requests tooa low value is strongly discouraged and may result in performance degradation.</span></span>

<span data-ttu-id="18385-879">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-879">Key information:</span></span>

- <span data-ttu-id="18385-880">이 값은 0을 포함한 양의 정수로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-880">Specify this value as a whole integer.</span></span>
- <span data-ttu-id="18385-881">지정 된 hello에 쉼표 또는 마침표를 포함 하지 마십시오 값입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-881">Do not include commas or periods in hello specified value.</span></span>

<span data-ttu-id="18385-882">**기본값:** 10,000개 요청</span><span class="sxs-lookup"><span data-stu-id="18385-882">**Default Value:** 10,000 requests</span></span>

###<a name="proxy-special-headers"></a><span data-ttu-id="18385-883">프록시 특별 헤더</span><span class="sxs-lookup"><span data-stu-id="18385-883">Proxy Special Headers</span></span>
<span data-ttu-id="18385-884">**목적:** hello 집합 정의 [CDN에 관련 된 요청 헤더]() 는 지 서버 tooan 원본 서버에서 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-884">**Purpose:** Defines hello set of [CDN-specific request headers]() that will be forwarded from an edge server tooan origin server.</span></span>

<span data-ttu-id="18385-885">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-885">Key information:</span></span>

- <span data-ttu-id="18385-886">이 기능에 정의 된 각 특정 CDN 요청 헤더 tooan 원본 서버에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-886">Each CDN-specific request header defined in this feature will be forwarded tooan origin server.</span></span>
- <span data-ttu-id="18385-887">이 목록에서 제거 하 여 원본 서버에 tooan 전달을 특정 CDN 요청 헤더를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-887">Prevent a CDN-specific request header from being forwarded tooan origin server by removing it from this list.</span></span>

<span data-ttu-id="18385-888">**기본 동작:** 모든 [CDN에 관련 된 요청 헤더]() toohello 원본 서버에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-888">**Default Behavior:** All [CDN-specific request headers]() will be forwarded toohello origin server.</span></span>

## <a name="specialty"></a><span data-ttu-id="18385-889">특별 사항</span><span class="sxs-lookup"><span data-stu-id="18385-889">Specialty</span></span>

<span data-ttu-id="18385-890">이러한 기능은 고급 사용자만 사용해야 하는 고급 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-890">These features provide advanced functionality that should only be used by advanced users.</span></span>

<span data-ttu-id="18385-891">이름</span><span class="sxs-lookup"><span data-stu-id="18385-891">Name</span></span> | <span data-ttu-id="18385-892">목적</span><span class="sxs-lookup"><span data-stu-id="18385-892">Purpose</span></span>
-----|--------
<span data-ttu-id="18385-893">캐시 가능한 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="18385-893">Cacheable HTTP Methods</span></span> | <span data-ttu-id="18385-894">Hello 네트워크에 캐시 될 수 있는 추가 HTTP 메서드 집합을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-894">Determines hello set of additional HTTP methods that can be cached on our network.</span></span>
<span data-ttu-id="18385-895">캐시 가능한 요청 본문 크기</span><span class="sxs-lookup"><span data-stu-id="18385-895">Cacheable Request Body Size</span></span> | <span data-ttu-id="18385-896">POST 응답을 캐시할 수 있는지 여부를 확인 하기 위한 hello 임계값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-896">Defines hello threshold for determining whether a POST response can be cached.</span></span>

###<a name="cacheable-http-methods"></a><span data-ttu-id="18385-897">캐시 가능한 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="18385-897">Cacheable HTTP Methods</span></span>
<span data-ttu-id="18385-898">**목적:** hello 네트워크에 캐시 될 수 있는 추가 HTTP 메서드 집합을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-898">**Purpose:** Determines hello set of additional HTTP methods that can be cached on our network.</span></span>

<span data-ttu-id="18385-899">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-899">Key information:</span></span>

- <span data-ttu-id="18385-900">이 기능은 GET 응답을 항상 캐시해야 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-900">This feature assumes that GET responses should always be cached.</span></span> <span data-ttu-id="18385-901">결과적으로, hello GET HTTP 메서드 설정이 기능이 포함 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-901">As a result, hello GET HTTP method should not be included when setting this feature.</span></span>
- <span data-ttu-id="18385-902">이 기능은 hello POST HTTP 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-902">This feature only supports hello POST HTTP method.</span></span> <span data-ttu-id="18385-903">이 기능을 :POST로 설정하여 POST 응답 캐싱을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-903">Enable POST response caching by setting this feature to:POST</span></span> 
- <span data-ttu-id="18385-904">기본적으로 본문이 14Kb 미만인 요청만 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-904">By default, only requests whose body is smaller than 14 Kb will be cached.</span></span> <span data-ttu-id="18385-905">Hello 최대 요청 본문 크기를 설정 하려면 캐시 가능한 요청 본문 크기 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-905">Use the Cacheable Request Body Size Feature to set hello maximum request body size.</span></span>

<span data-ttu-id="18385-906">**기본 동작:** GET 응답만 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-906">**Default Behavior:** Only GET responses will be cached.</span></span>

###<a name="cacheable-request-body-size"></a><span data-ttu-id="18385-907">캐시 가능한 요청 본문 크기</span><span class="sxs-lookup"><span data-stu-id="18385-907">Cacheable Request Body Size</span></span>

<span data-ttu-id="18385-908">**목적:** POST 응답을 캐시할 수 있는지 여부를 확인 하기 위한 hello 임계값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-908">**Purpose:** Defines hello threshold for determining whether a POST response can be cached.</span></span>

<span data-ttu-id="18385-909">이 임계값은 최대 요청 본문 크기를 지정하여 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-909">This threshold is determined by specifying a maximum request body size.</span></span> <span data-ttu-id="18385-910">더 큰 요청 본문을 포함한 요청은 캐시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-910">Requests that contain a larger request body will not be cached.</span></span>

<span data-ttu-id="18385-911">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-911">Key information:</span></span>

- <span data-ttu-id="18385-912">POST 응답이 캐싱에 적합한 경우에만 이 기능을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-912">This Feature is only applicable when POST responses are eligible for caching.</span></span> <span data-ttu-id="18385-913">Hello 캐시 가능한 HTTP 메서드에 기능을 사용 하 여 POST 요청 캐싱을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-913">Use hello Cacheable HTTP Methods Feature to enable POST request caching.</span></span>
- <span data-ttu-id="18385-914">hello 요청 본문에 대 한에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-914">hello request body is taken into consideration for:</span></span>
    - <span data-ttu-id="18385-915">x-www-form-urlencoded 값</span><span class="sxs-lookup"><span data-stu-id="18385-915">x-www-form-urlencoded values</span></span>
    - <span data-ttu-id="18385-916">고유한 cache-key 보장</span><span class="sxs-lookup"><span data-stu-id="18385-916">Ensuring a unique cache-key</span></span>
- <span data-ttu-id="18385-917">최대 요청 본문 크기를 크게 정의하면 데이터 전달 성능에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-917">Defining a large maximum request body size may impact data delivery performance.</span></span>
    - <span data-ttu-id="18385-918">**권장되는 값:** 14Kb</span><span class="sxs-lookup"><span data-stu-id="18385-918">**Recommended Value:** 14 Kb</span></span>
    - <span data-ttu-id="18385-919">**최소값:** 1Kb</span><span class="sxs-lookup"><span data-stu-id="18385-919">**Minimum Value:** 1 Kb</span></span>

<span data-ttu-id="18385-920">**기본 동작:** 14Kb</span><span class="sxs-lookup"><span data-stu-id="18385-920">**Default Behavior:** 14 Kb</span></span>
 
## <a name="url"></a><span data-ttu-id="18385-921">URL</span><span class="sxs-lookup"><span data-stu-id="18385-921">URL</span></span>

<span data-ttu-id="18385-922">이러한 기능을 통해 요청 toobe 리디렉션되거나 tooa 다른 URL을 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-922">These features allow a request toobe redirected or rewritten tooa different URL.</span></span>

<span data-ttu-id="18385-923">이름</span><span class="sxs-lookup"><span data-stu-id="18385-923">Name</span></span> | <span data-ttu-id="18385-924">목적</span><span class="sxs-lookup"><span data-stu-id="18385-924">Purpose</span></span>
-----|--------
<span data-ttu-id="18385-925">리디렉션 추적</span><span class="sxs-lookup"><span data-stu-id="18385-925">Follow Redirects</span></span> | <span data-ttu-id="18385-926">요청 고객 원본 서버에서 반환 되는 hello 위치 헤더에 정의 된 리디렉션된 toohello hostname 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-926">Determines whether requests can be redirected toohello hostname defined in hello Location header returned by a customer origin server.</span></span>
<span data-ttu-id="18385-927">URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="18385-927">URL Redirect</span></span> | <span data-ttu-id="18385-928">Hello 위치 헤더를 통해 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-928">Redirects requests via hello Location header.</span></span>
<span data-ttu-id="18385-929">URL 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-929">URL Rewrite</span></span>  | <span data-ttu-id="18385-930">Hello 요청 URL을 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-930">Rewrites hello request URL.</span></span>

###<a name="follow-redirects"></a><span data-ttu-id="18385-931">리디렉션 추적</span><span class="sxs-lookup"><span data-stu-id="18385-931">Follow Redirects</span></span>
<span data-ttu-id="18385-932">**목적:** 요청 하는 고객 원본 서버에서 반환 되는 위치 헤더에 정의 된 리디렉션된 toohello hostname이 될 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-932">**Purpose:** Determines whether requests can be redirected toohello hostname defined in the Location header returned by a customer origin server.</span></span>

<span data-ttu-id="18385-933">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-933">Key information:</span></span>

- <span data-ttu-id="18385-934">요청에 리디렉션된 tooedge CNAMEs toohello 해당 하는 수만 있습니다 동일한 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-934">Requests can only be redirected tooedge CNAMEs that correspond toohello same platform.</span></span>

<span data-ttu-id="18385-935">값</span><span class="sxs-lookup"><span data-stu-id="18385-935">Value</span></span>|<span data-ttu-id="18385-936">결과</span><span class="sxs-lookup"><span data-stu-id="18385-936">Result</span></span>
-|-
<span data-ttu-id="18385-937">사용</span><span class="sxs-lookup"><span data-stu-id="18385-937">Enabled</span></span>|<span data-ttu-id="18385-938">요청을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-938">Requests can be redirected.</span></span>
<span data-ttu-id="18385-939">사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-939">Disabled</span></span>|<span data-ttu-id="18385-940">요청을 리디렉션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-940">Requests will not be redirected.</span></span>

<span data-ttu-id="18385-941">**기본 동작**: 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="18385-941">**Default Behavior:** Disabled.</span></span>
###<a name="url-redirect"></a><span data-ttu-id="18385-942">URL 리디렉션</span><span class="sxs-lookup"><span data-stu-id="18385-942">URL Redirect</span></span>
<span data-ttu-id="18385-943">**목적:** Location 헤더를 통해 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-943">**Purpose:** Redirects requests via the Location header.</span></span>

<span data-ttu-id="18385-944">이 기능의 hello 구성 hello 다음 옵션을 설정 하는 사항이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-944">hello configuration of this feature requires setting hello following options:</span></span>

<span data-ttu-id="18385-945">옵션</span><span class="sxs-lookup"><span data-stu-id="18385-945">Option</span></span>|<span data-ttu-id="18385-946">설명</span><span class="sxs-lookup"><span data-stu-id="18385-946">Description</span></span>
-|-
<span data-ttu-id="18385-947">코드</span><span class="sxs-lookup"><span data-stu-id="18385-947">Code</span></span>|<span data-ttu-id="18385-948">Toohello 요청자에 게 반환 되는 hello 응답 코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-948">Select hello response code that will be returned toohello requester.</span></span>
<span data-ttu-id="18385-949">원본 및 패턴</span><span class="sxs-lookup"><span data-stu-id="18385-949">Source & Pattern</span></span>| <span data-ttu-id="18385-950">이러한 설정은 트리로 이동 될 수 있는 요청 hello 형식을 식별 하는 요청 URI 패턴을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-950">These settings define a request URI pattern that identifies hello type of requests that may be redirected.</span></span> <span data-ttu-id="18385-951">URL의 기준에 따라 hello 둘 모두를 충족 하는 유일한 요청이 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-951">Only requests whose URL satisfies both of hello following criteria will be redirected:</span></span> <br/> <br/> <span data-ttu-id="18385-952">**원본:**(또는 콘텐츠 액세스 지점) 원본 서버를 식별하는 상대 경로를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-952">**Source :** (or content access point) Select a relative path that identifies an origin server.</span></span> <span data-ttu-id="18385-953">이것이 hello "/XXXX/" 섹션 및 끝점 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-953">This is hello  "/XXXX/" section and your endpoint name.</span></span> <br/> <span data-ttu-id="18385-954">**원본(패턴):** 상대 경로로 요청을 식별하는 패턴을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-954">**Source (pattern):** A pattern that identifies requests by relative path must be defined.</span></span> <span data-ttu-id="18385-955">이 정규식 패턴 hello 이전에 콘텐츠 액세스 지점 (위 참조)를 선택한 후 바로 시작 하는 경로 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-955">This regular expression pattern must define a path that starts directly after hello previously selected content access point (see above).</span></span> <br/> <span data-ttu-id="18385-956">-있는지 확인 하십시오 (즉, 소스 및 패턴) hello 요청 URI 조건 위에 정의 된는이 기능에 대해 정의 된 모든 일치 조건을 충돌 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-956">- Make sure that hello request URI criteria (i.e., Source & Pattern) defined above doesn't conflict with any match conditions defined for this feature.</span></span> <br/> <span data-ttu-id="18385-957">-있는지 toospecify 패턴을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-957">- Make sure toospecify a pattern.</span></span> <span data-ttu-id="18385-958">Hello 패턴으로 빈 값을 사용 하 여 요청 toohello 서버의 루트 폴더에 hello 선택한 원본 (예: http://cdn.mydomain.com/)만 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-958">Using a blank value as hello pattern will only match requests toohello root folder of hello selected origin server (e.g., http://cdn.mydomain.com/).</span></span>
<span data-ttu-id="18385-959">대상</span><span class="sxs-lookup"><span data-stu-id="18385-959">Destination</span></span>| <span data-ttu-id="18385-960">Hello URL은 정의 요청 위에 toowhich hello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-960">Define hello URL toowhich hello above requests will be redirected.</span></span> <br/> <span data-ttu-id="18385-961">다음을 사용하여 이 URL을 동적으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-961">Dynamically construct this URL using:</span></span> <br/> <span data-ttu-id="18385-962">- 정규식 패턴</span><span class="sxs-lookup"><span data-stu-id="18385-962">- A regular expression pattern</span></span> <br/><span data-ttu-id="18385-963">- HTTP 변수</span><span class="sxs-lookup"><span data-stu-id="18385-963">- HTTP variables</span></span> <br/> <span data-ttu-id="18385-964">$를 사용 하 여 hello 대상 패턴에 캡처되며, hello 소스 패턴에서 hello 값으로 대체 _n_  여기서  _n_  캡처되는 hello 순서에 따라 값을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-964">Substitute hello values captured in hello source pattern into hello destination pattern using $_n_ where _n_ identifies a value by hello order in which it was captured.</span></span> <span data-ttu-id="18385-965">예를 들어 $1 hello $2 hello 두 번째 값을 나타내는 동안 hello 소스 패턴에서 캡처되는 첫 번째 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18385-965">For example, $1 represents hello first value captured in hello source pattern, while $2 represents hello second value.</span></span> <br/> 
<span data-ttu-id="18385-966">이 뛰어납니다 toouse 절대 URL을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-966">It is highly recommended toouse an absolute URL.</span></span> <span data-ttu-id="18385-967">상대 URL의 hello 사용 CDN Url tooan 잘못 된 경로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-967">hello use of a relative URL may redirect CDN URLs tooan invalid path.</span></span>

<span data-ttu-id="18385-968">**샘플 시나리오**</span><span class="sxs-lookup"><span data-stu-id="18385-968">**Sample Scenario**</span></span>

<span data-ttu-id="18385-969">이 예제에서는 보여 줍니다 tooredirect 가장자리 toothis 확인 되는 CNAME URL의 CDN URL 기본 방법: http://marketing.azureedge.net/brochures</span><span class="sxs-lookup"><span data-stu-id="18385-969">In this example, we will demonstrate how tooredirect an edge CNAME URL that resolves toothis base CDN URL: http://marketing.azureedge.net/brochures</span></span>

<span data-ttu-id="18385-970">기본 가장자리 CNAME URL 리디렉션된 toothis 됩니다 요청을 한 정하는: http://cdn.mydomain.com/resources</span><span class="sxs-lookup"><span data-stu-id="18385-970">Qualifying requests will be redirected toothis base edge CNAME URL: http://cdn.mydomain.com/resources</span></span>

<span data-ttu-id="18385-971">이 URL 리디렉션 같은 구성이 hello를 통해 수행할 수 있습니다.![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)</span><span class="sxs-lookup"><span data-stu-id="18385-971">This URL redirection may be achieved through hello following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)</span></span>

<span data-ttu-id="18385-972">**주요 정보:**</span><span class="sxs-lookup"><span data-stu-id="18385-972">**Key points:**</span></span>

- <span data-ttu-id="18385-973">hello URL 리디렉션 기능 정의 hello 요청 리디렉션될 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-973">hello URL Redirect feature defines hello request URLs that will be redirected.</span></span> <span data-ttu-id="18385-974">따라서 추가적인 일치 조건이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-974">As a result, additional match conditions are not required.</span></span> <span data-ttu-id="18385-975">Hello 일치 조건을 "Always"로 정의 되지만 해당 지점 toohello "브로슈어" hello "마케팅" 고객 원본에 대 한 폴더 리디렉션 됨 권한만 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-975">Although hello match condition was defined as "Always," only requests that point toohello "brochures" folder on hello "marketing" customer origin will be redirected.</span></span> 
- <span data-ttu-id="18385-976">일치 하는 모든 요청에 리디렉션된 toohello 가장자리 CNAME URL 대상 옵션에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-976">All matching requests will be redirected toohello edge CNAME URL defined in the Destination option.</span></span> 
    - <span data-ttu-id="18385-977">샘플 시나리오 #1:</span><span class="sxs-lookup"><span data-stu-id="18385-977">Sample scenario #1:</span></span> 
        - <span data-ttu-id="18385-978">샘플 요청(CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="18385-978">Sample request (CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf</span></span> 
        - <span data-ttu-id="18385-979">요청 URL(리디렉션 이후): http://cdn.mydomain.com/resources/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="18385-979">Request URL (after redirect): http://cdn.mydomain.com/resources/widgets.pdf</span></span>  
    - <span data-ttu-id="18385-980">샘플 시나리오 2:</span><span class="sxs-lookup"><span data-stu-id="18385-980">Sample scenario #2:</span></span> 
        - <span data-ttu-id="18385-981">샘플 요청(에지 CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="18385-981">Sample request (Edge CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf</span></span> 
        - <span data-ttu-id="18385-982">요청 URL(리디렉션 이후): http://cdn.mydomain.com/resources/widgets.pdf 샘플 시나리오</span><span class="sxs-lookup"><span data-stu-id="18385-982">Request URL (after redirect): http://cdn.mydomain.com/resources/widgets.pdf  Sample scenario</span></span>
    - <span data-ttu-id="18385-983">샘플 시나리오 #3:</span><span class="sxs-lookup"><span data-stu-id="18385-983">Sample scenario #3:</span></span> 
        - <span data-ttu-id="18385-984">샘플 요청(에지 CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt</span><span class="sxs-lookup"><span data-stu-id="18385-984">Sample request (Edge CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt</span></span> 
        - <span data-ttu-id="18385-985">요청 URL(리디렉션 이후):: http://cdn.mydomain.com/resources/campaignA/final/productC.ppt</span><span class="sxs-lookup"><span data-stu-id="18385-985">Request URL (after redirect): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt</span></span>  
- <span data-ttu-id="18385-986">hello 요청 체계 (% {scheme}) 변수는 대상 옵션에서 활용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-986">hello Request Scheme (%{scheme}) variable was leveraged in the Destination option.</span></span> <span data-ttu-id="18385-987">이렇게 하면 해당 hello 요청 체계 리디렉션 후 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-987">This ensures that hello request's scheme remains unchanged after redirection.</span></span>
- <span data-ttu-id="18385-988">hello 요청에서 캡처된 hello URL 세그먼트는 "$1."를 통해 추가 된 toohello 새 URL</span><span class="sxs-lookup"><span data-stu-id="18385-988">hello URL segments that were captured from hello request are appended toohello new URL via "$1."</span></span>
 
###<a name="url-rewrite"></a><span data-ttu-id="18385-989">URL 다시 쓰기</span><span class="sxs-lookup"><span data-stu-id="18385-989">URL Rewrite</span></span>
<span data-ttu-id="18385-990">**목적:** hello 요청 URL을 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-990">**Purpose:** Rewrites hello request URL.</span></span>

<span data-ttu-id="18385-991">주요 정보:</span><span class="sxs-lookup"><span data-stu-id="18385-991">Key information:</span></span>

- <span data-ttu-id="18385-992">이 기능의 hello 구성 hello 다음 옵션을 설정 하는 사항이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-992">hello configuration of this feature requires setting hello following options:</span></span>

<span data-ttu-id="18385-993">옵션</span><span class="sxs-lookup"><span data-stu-id="18385-993">Option</span></span>|<span data-ttu-id="18385-994">설명</span><span class="sxs-lookup"><span data-stu-id="18385-994">Description</span></span>
-|-
 <span data-ttu-id="18385-995">원본 및 패턴</span><span class="sxs-lookup"><span data-stu-id="18385-995">Source & Pattern</span></span> | <span data-ttu-id="18385-996">이러한 설정은 다시 작성 하는 요청의 hello 형식을 식별 하는 요청 URI 패턴을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-996">These settings define a request URI pattern that identifies hello type of requests that may be rewritten.</span></span> <span data-ttu-id="18385-997">URL의 기준에 따라 hello 둘 모두를 충족 하는 유일한 요청 다시 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-997">Only requests whose URL satisfies both of hello following criteria will be rewritten:</span></span> <br/>     <span data-ttu-id="18385-998">- **원본(또는 콘텐츠 액세스 지점):** 원본 서버를 식별하는 상대 경로를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-998">- **Source (or content access point):** Select a relative path that identifies an origin server.</span></span> <span data-ttu-id="18385-999">이것이 hello "/XXXX/" 섹션 및 끝점 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18385-999">This is hello  "/XXXX/" section and your endpoint name.</span></span> <br/> <span data-ttu-id="18385-1000">- **원본(패턴):** 상대 경로로 요청을 식별하는 패턴을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1000">- **Source (pattern):** A pattern that identifies requests by relative path must be defined.</span></span> <span data-ttu-id="18385-1001">이 정규식 패턴 hello 이전에 콘텐츠 액세스 지점 (위 참조)를 선택한 후 바로 시작 하는 경로 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1001">This regular expression pattern must define a path that starts directly after hello previously selected content access point (see above).</span></span> <br/> <span data-ttu-id="18385-1002">Hello 요청 URI 조건 (예: 소스 및 패턴) 위에 정의 된이 기능에 대해 정의 된 hello 일치 조건 중 하나라도와 충돌 하지 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1002">Make sure that hello request URI criteria (i.e., Source & Pattern) defined above doesn't conflict with any of hello match conditions defined for this feature.</span></span> <span data-ttu-id="18385-1003">있는지 toospecify 패턴을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1003">Make sure toospecify a pattern.</span></span> <span data-ttu-id="18385-1004">Hello 패턴으로 빈 값을 사용 하 여 요청 toohello 서버의 루트 폴더에 hello 선택한 원본 (예: http://cdn.mydomain.com/)만 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1004">Using a blank value as hello pattern will only match requests toohello root folder of hello selected origin server (e.g., http://cdn.mydomain.com/).</span></span> 
 <span data-ttu-id="18385-1005">대상</span><span class="sxs-lookup"><span data-stu-id="18385-1005">Destination</span></span>  |<span data-ttu-id="18385-1006">Hello 상대 URL을 정의 하 여 요청 위에 toowhich hello를 다시 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1006">Define hello relative URL toowhich hello above requests will be rewritten by:</span></span> <br/>    <span data-ttu-id="18385-1007">1. 원본 서버를 식별하는 콘텐츠 액세스 지점 선택</span><span class="sxs-lookup"><span data-stu-id="18385-1007">1. Selecting a content access point that identifies an origin server.</span></span> <br/>    <span data-ttu-id="18385-1008">2. 다음을 사용하여 상대 경로 정의</span><span class="sxs-lookup"><span data-stu-id="18385-1008">2. Defining a relative path using:</span></span> <br/>        <span data-ttu-id="18385-1009">- 정규식 패턴</span><span class="sxs-lookup"><span data-stu-id="18385-1009">- A regular expression pattern</span></span> <br/>        <span data-ttu-id="18385-1010">- HTTP 변수</span><span class="sxs-lookup"><span data-stu-id="18385-1010">- HTTP variables</span></span> <br/> <br/> <span data-ttu-id="18385-1011">$를 사용 하 여 hello 대상 패턴에 캡처되며, hello 소스 패턴에서 hello 값으로 대체 _n_  여기서  _n_  캡처되는 hello 순서에 따라 값을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1011">Substitute hello values captured in hello source pattern into hello destination pattern using $_n_ where _n_ identifies a value by hello order in which it was captured.</span></span> <span data-ttu-id="18385-1012">예를 들어 $1 hello $2 hello 두 번째 값을 나타내는 동안 hello 소스 패턴에서 캡처되는 첫 번째 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1012">For example, $1 represents hello first value captured in hello source pattern, while $2 represents hello second value.</span></span> 
 <span data-ttu-id="18385-1013">이 기능 edge 서버 toorewrite hello URL을 기존의 리디렉션을 수행 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1013">This feature allows our edge servers toorewrite hello URL without performing a traditional redirect.</span></span> <span data-ttu-id="18385-1014">즉, 해당 hello 요청자 hello hello를 다시 작성 URL에 요청 하는 경우 같은 응답 코드를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1014">This means that hello requester will receive hello same response code as if hello rewritten URL had been requested.</span></span>

<span data-ttu-id="18385-1015">**샘플 시나리오 1**</span><span class="sxs-lookup"><span data-stu-id="18385-1015">**Sample Scenario 1**</span></span>

<span data-ttu-id="18385-1016">이 예제에서는 보여 줍니다 tooredirect 가장자리 toothis 확인 되는 CNAME URL의 CDN URL 기본 방법: http://marketing.azureedge.net/brochures/</span><span class="sxs-lookup"><span data-stu-id="18385-1016">In this example, we will demonstrate how tooredirect an edge CNAME URL that resolves toothis base CDN URL: http://marketing.azureedge.net/brochures/</span></span>

<span data-ttu-id="18385-1017">기본 가장자리 CNAME URL 리디렉션된 toothis 됩니다 요청을 한 정하는: http://MyOrigin.azureedge.net/resources/</span><span class="sxs-lookup"><span data-stu-id="18385-1017">Qualifying requests will be redirected toothis base edge CNAME URL: http://MyOrigin.azureedge.net/resources/</span></span>

<span data-ttu-id="18385-1018">이 URL 리디렉션 같은 구성이 hello를 통해 수행할 수 있습니다.![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)</span><span class="sxs-lookup"><span data-stu-id="18385-1018">This URL redirection may be achieved through hello following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)</span></span>

<span data-ttu-id="18385-1019">**샘플 시나리오 2**</span><span class="sxs-lookup"><span data-stu-id="18385-1019">**Sample Scenario 2**</span></span>

<span data-ttu-id="18385-1020">이 예에서 보여 드리겠습니다 방법을 tooredirect 정규식을 사용 하는 대문자 toolowercase에서 CNAME URL 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1020">In this example, we will demonstrate how tooredirect an edge CNAME URL from UPPERCASE toolowercase using regular expressions.</span></span>

<span data-ttu-id="18385-1021">이 URL 리디렉션 같은 구성이 hello를 통해 수행할 수 있습니다.![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)</span><span class="sxs-lookup"><span data-stu-id="18385-1021">This URL redirection may be achieved through hello following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)</span></span>


<span data-ttu-id="18385-1022">**주요 정보:**</span><span class="sxs-lookup"><span data-stu-id="18385-1022">**Key points:**</span></span>

- <span data-ttu-id="18385-1023">hello URL 재작성 기능 hello을 정의 하는 다시 작성 하는 Url을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1023">hello URL Rewrite feature defines hello request URLs that will be rewritten.</span></span> <span data-ttu-id="18385-1024">따라서 추가적인 일치 조건이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1024">As a result, additional match conditions are not required.</span></span> <span data-ttu-id="18385-1025">Hello 일치 조건을 "Always"로 정의 되지만 해당 지점 toohello "브로슈어" hello "마케팅" 고객 원본에 대 한 폴더를 다시 작성 됩니다 권한만 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1025">Although hello match condition was defined as "Always," only requests that point toohello "brochures" folder on hello "marketing" customer origin will be rewritten.</span></span>

- <span data-ttu-id="18385-1026">hello 요청에서 캡처된 hello URL 세그먼트는 "$1."를 통해 추가 된 toohello 새 URL</span><span class="sxs-lookup"><span data-stu-id="18385-1026">hello URL segments that were captured from hello request are appended toohello new URL via "$1."</span></span>



###<a name="compatibility"></a><span data-ttu-id="18385-1027">호환성</span><span class="sxs-lookup"><span data-stu-id="18385-1027">Compatibility</span></span>

<span data-ttu-id="18385-1028">이 기능이 적용 된 tooa 요청 수 전에 충족 해야 하는 조건과 일치 하는 것을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1028">This feature includes matching criteria that must be met before it can be applied tooa request.</span></span> <span data-ttu-id="18385-1029">충돌 하는 조건에 맞는를 순서 tooprevent 설정,이 기능은 일치 조건을 다음 hello와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18385-1029">In order tooprevent setting up conflicting match criteria, this feature is incompatible with hello following match conditions:</span></span>

- <span data-ttu-id="18385-1030">AS 숫자</span><span class="sxs-lookup"><span data-stu-id="18385-1030">AS Number</span></span>
- <span data-ttu-id="18385-1031">CDN 원본</span><span class="sxs-lookup"><span data-stu-id="18385-1031">CDN Origin</span></span>
- <span data-ttu-id="18385-1032">클라이언트 IP 주소</span><span class="sxs-lookup"><span data-stu-id="18385-1032">Client IP Address</span></span>
- <span data-ttu-id="18385-1033">고객 원본</span><span class="sxs-lookup"><span data-stu-id="18385-1033">Customer Origin</span></span>
- <span data-ttu-id="18385-1034">요청 스키마</span><span class="sxs-lookup"><span data-stu-id="18385-1034">Request Scheme</span></span>
- <span data-ttu-id="18385-1035">URL 경로 디렉터리</span><span class="sxs-lookup"><span data-stu-id="18385-1035">URL Path Directory</span></span>
- <span data-ttu-id="18385-1036">URL 경로 확장</span><span class="sxs-lookup"><span data-stu-id="18385-1036">URL Path Extension</span></span>
- <span data-ttu-id="18385-1037">URL 경로 파일 이름</span><span class="sxs-lookup"><span data-stu-id="18385-1037">URL Path Filename</span></span>
- <span data-ttu-id="18385-1038">URL 경로 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-1038">URL Path Literal</span></span>
- <span data-ttu-id="18385-1039">URL 경로 Regex</span><span class="sxs-lookup"><span data-stu-id="18385-1039">URL Path Regex</span></span>
- <span data-ttu-id="18385-1040">URL 경로 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-1040">URL Path Wildcard</span></span>
- <span data-ttu-id="18385-1041">URL 쿼리 리터럴</span><span class="sxs-lookup"><span data-stu-id="18385-1041">URL Query Literal</span></span>
- <span data-ttu-id="18385-1042">URL 쿼리 매개 변수</span><span class="sxs-lookup"><span data-stu-id="18385-1042">URL Query Parameter</span></span>
- <span data-ttu-id="18385-1043">URL 쿼리 Regex</span><span class="sxs-lookup"><span data-stu-id="18385-1043">URL Query Regex</span></span>
- <span data-ttu-id="18385-1044">URL 쿼리 와일드카드</span><span class="sxs-lookup"><span data-stu-id="18385-1044">URL Query Wildcard</span></span>


## <a name="next-steps"></a><span data-ttu-id="18385-1045">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18385-1045">Next Steps</span></span>
* [<span data-ttu-id="18385-1046">규칙 엔진 참조</span><span class="sxs-lookup"><span data-stu-id="18385-1046">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="18385-1047">규칙 엔진 조건식</span><span class="sxs-lookup"><span data-stu-id="18385-1047">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="18385-1048">규칙 엔진 일치 조건</span><span class="sxs-lookup"><span data-stu-id="18385-1048">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="18385-1049">Hello 규칙 엔진을 사용 하 여 기본 HTTP 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="18385-1049">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* [<span data-ttu-id="18385-1050">Azure CDN 개요</span><span class="sxs-lookup"><span data-stu-id="18385-1050">Azure CDN Overview</span></span>](cdn-overview.md)
