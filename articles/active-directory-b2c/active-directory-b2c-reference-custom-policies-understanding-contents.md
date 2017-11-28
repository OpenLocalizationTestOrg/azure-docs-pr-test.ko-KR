---
title: "Azure Active Directory B2C: hello 스타터 팩의 사용자 지정 정책 이해 | Microsoft Docs"
description: "Azure Active Directory B2C 사용자 지정 정책에 대한 항목"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="ac34a-103">Azure AD B2C hello 정책 사용자 지정 스타터 팩의 사용자 지정 정책 hello 이해</span><span class="sxs-lookup"><span data-stu-id="ac34a-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="ac34a-104">이 섹션에서는 hello와 함께 제공 하는 hello B2C_1A_base 정책의 모든 hello 코어 요소 **스타터 팩** hello의 hello 상속을 통해 직접 정책을 작성에 대 한를 활용 하 고 *B2C_1A_base_ 확장명 정책*합니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="ac34a-105">이와 같이 더 특히 집중적으로 다룹니다 hello 이미 정의 된 클레임 형식, 클레임 변환을, 콘텐츠 정의 클레임 공급자에 게 자신의 기술 프로필 하 고 핵심 사용자 여정이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac34a-106">Microsoft는 어떠한 명시적 이거나 묵시적인 보증도 하지 않습니다이 제공 된 기준 toohello 정보를는.</span><span class="sxs-lookup"><span data-stu-id="ac34a-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="ac34a-107">GA 시간 이전, GA 시간 또는 그 이후에 언제든지 변경 사항을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="ac34a-108">사용자 고유의 정책 및 hello B2C_1A_base_extensions 정책 수 이러한 정의 무시 하 고 필요에 따라 추가 구성을 제공 하 여이 부모 정책을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="ac34a-109">hello의 핵심 요소 hello *B2C_1A_base 정책* 클레임 형식과 클레임 변환을 콘텐츠 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="ac34a-110">이러한 요소에도 hello와 같이 사용자 고유의 정책에서 참조 되는 취약 toobe 수 *B2C_1A_base_extensions 정책*합니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="ac34a-111">클레임 스키마</span><span class="sxs-lookup"><span data-stu-id="ac34a-111">Claims schemas</span></span>

<span data-ttu-id="ac34a-112">이 스키마는 다음과 같은 세 가지 섹션으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="ac34a-113">Hello 최소 데 필요한 클레임을 사용자 여정이 toowork hello에 대 한 제대로 나열 하는 첫 번째 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="ac34a-114">두 번째 섹션 목록에 쿼리 문자열 매개 변수가 필요한 클레임 hello 및 기타 특수 매개 변수 toobe 전달 tooother 클레임 공급자 인증을 위해 특히 login.microsoftonline.com입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="ac34a-115">**이러한 클레임을 수정하지 마세요**.</span><span class="sxs-lookup"><span data-stu-id="ac34a-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="ac34a-116">되 고 hello 사용자 로부터 수집할 수 있는 추가, 선택적 클레임을 나열 하는 세 번째 섹션 hello 디렉터리에 저장 하는 동안 로그인 토큰에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="ac34a-117">이 섹션에 유형 toobe hello 사용자 로부터 수집 및/또는 hello 토큰에 전송 하는 새 클레임을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac34a-118">hello 클레임 스키마 암호와 사용자 이름을 같은 특정 클레임에 대 한 제한을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="ac34a-119">hello 신뢰 프레임 워크 (TF) 정책 다른 클레임 공급자와 Azure AD를 취급 하 고 hello 프리미엄 정책에 해당 하는 모든 제한은 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="ac34a-120">정책이 수정된 tooadd 더 많은 제한이 또는 고유 제한 사항을 포함 하는 자격 증명 저장소에 대 한 다른 클레임 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="ac34a-121">아래 hello 사용 가능한 클레임 유형이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="ac34a-122">Hello 사용자 친구에 필요한 클레임</span><span class="sxs-lookup"><span data-stu-id="ac34a-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="ac34a-123">다음 클레임 hello가 제대로 사용자 여정이 toowork 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="ac34a-124">클레임 유형</span><span class="sxs-lookup"><span data-stu-id="ac34a-124">Claims type</span></span> | <span data-ttu-id="ac34a-125">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="ac34a-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-126">*UserId*</span></span> | <span data-ttu-id="ac34a-127">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="ac34a-127">Username</span></span> |
| <span data-ttu-id="ac34a-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="ac34a-128">*signInName*</span></span> | <span data-ttu-id="ac34a-129">로그인 이름</span><span class="sxs-lookup"><span data-stu-id="ac34a-129">Sign in name</span></span> |
| <span data-ttu-id="ac34a-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-130">*tenantId*</span></span> | <span data-ttu-id="ac34a-131">Azure AD B2C 프리미엄에 hello 사용자 개체의 테 넌 트 식별자 (ID)</span><span class="sxs-lookup"><span data-stu-id="ac34a-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="ac34a-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-132">*objectId*</span></span> | <span data-ttu-id="ac34a-133">Azure AD B2C 프리미엄에 hello 사용자 개체의 개체 식별자 (ID)</span><span class="sxs-lookup"><span data-stu-id="ac34a-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="ac34a-134">*암호*</span><span class="sxs-lookup"><span data-stu-id="ac34a-134">*password*</span></span> | <span data-ttu-id="ac34a-135">암호</span><span class="sxs-lookup"><span data-stu-id="ac34a-135">Password</span></span> |
| <span data-ttu-id="ac34a-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="ac34a-136">*newPassword*</span></span> | |
| <span data-ttu-id="ac34a-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="ac34a-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="ac34a-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="ac34a-138">*passwordPolicies*</span></span> | <span data-ttu-id="ac34a-139">Azure AD B2C 프리미엄 toodetermine 암호 강도, 만료, 등에서 사용 하는 암호 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="ac34a-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="ac34a-140">*sub*</span></span> | |
| <span data-ttu-id="ac34a-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="ac34a-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="ac34a-142">*identityProvider*</span></span> | |
| <span data-ttu-id="ac34a-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="ac34a-143">*displayName*</span></span> | |
| <span data-ttu-id="ac34a-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="ac34a-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="ac34a-145">사용자의 전화 번호</span><span class="sxs-lookup"><span data-stu-id="ac34a-145">User's telephone number</span></span> |
| <span data-ttu-id="ac34a-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="ac34a-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="ac34a-147">*email*</span><span class="sxs-lookup"><span data-stu-id="ac34a-147">*email*</span></span> | <span data-ttu-id="ac34a-148">전자 메일 주소를 사용 하는 toocontact hello 사용자 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="ac34a-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="ac34a-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="ac34a-150">Hello 사용자 전자 메일 주소에 toosign צ ְ ײ</span><span class="sxs-lookup"><span data-stu-id="ac34a-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="ac34a-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="ac34a-151">*otherMails*</span></span> | <span data-ttu-id="ac34a-152">사용 되는 toocontact hello 사용자 일 수 있는 전자 메일 주소</span><span class="sxs-lookup"><span data-stu-id="ac34a-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="ac34a-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="ac34a-153">*userPrincipalName*</span></span> | <span data-ttu-id="ac34a-154">Azure AD B2C 프리미엄 hello에 저장 되어 있는 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="ac34a-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="ac34a-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="ac34a-155">*upnUserName*</span></span> | <span data-ttu-id="ac34a-156">사용자 계정 이름을 만들기 위한 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="ac34a-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="ac34a-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="ac34a-157">*mailNickName*</span></span> | <span data-ttu-id="ac34a-158">Azure AD B2C 프리미엄 hello에 저장 된 사용자의 메일 nick 이름</span><span class="sxs-lookup"><span data-stu-id="ac34a-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="ac34a-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="ac34a-159">*newUser*</span></span> | |
| <span data-ttu-id="ac34a-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="ac34a-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="ac34a-161">특성 hello 사용자 로부터 수집한 여부를 지정 하는 클레임</span><span class="sxs-lookup"><span data-stu-id="ac34a-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="ac34a-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="ac34a-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="ac34a-163">새 전화 번호를 hello 사용자 로부터 수집 된 있는지 여부를 지정 하는 클레임</span><span class="sxs-lookup"><span data-stu-id="ac34a-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="ac34a-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="ac34a-164">*authenticationSource*</span></span> | <span data-ttu-id="ac34a-165">Hello 사용자 소셜 Id 공급자, login.microsoftonline.com, 또는 로컬 계정에서 인증 되었는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="ac34a-166">쿼리 문자열 매개 변수 및 기타 특수 매개 변수에 필요한 클레임</span><span class="sxs-lookup"><span data-stu-id="ac34a-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="ac34a-167">hello 다음 클레임은 특수 한 매개 변수 (일부 쿼리 문자열 매개 변수 포함) tooother 클레임 공급자에 필요한 toopass:</span><span class="sxs-lookup"><span data-stu-id="ac34a-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="ac34a-168">클레임 유형</span><span class="sxs-lookup"><span data-stu-id="ac34a-168">Claims type</span></span> | <span data-ttu-id="ac34a-169">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="ac34a-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="ac34a-170">*nux*</span></span> | <span data-ttu-id="ac34a-171">인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ac34a-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="ac34a-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="ac34a-172">*nca*</span></span> | <span data-ttu-id="ac34a-173">인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ac34a-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="ac34a-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="ac34a-174">*prompt*</span></span> | <span data-ttu-id="ac34a-175">인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ac34a-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="ac34a-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="ac34a-176">*mkt*</span></span> | <span data-ttu-id="ac34a-177">인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ac34a-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="ac34a-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="ac34a-178">*lc*</span></span> | <span data-ttu-id="ac34a-179">인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ac34a-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="ac34a-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="ac34a-180">*grant_type*</span></span> | <span data-ttu-id="ac34a-181">인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ac34a-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="ac34a-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="ac34a-182">*scope*</span></span> | <span data-ttu-id="ac34a-183">인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ac34a-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="ac34a-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="ac34a-184">*client_id*</span></span> | <span data-ttu-id="ac34a-185">인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ac34a-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="ac34a-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="ac34a-186">*objectIdFromSession*</span></span> | <span data-ttu-id="ac34a-187">SSO 세션에서 검색 된 hello 기본 세션 관리 공급자 tooindicate hello 개체 id는에서 제공 하는 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac34a-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="ac34a-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="ac34a-188">*isActiveMFASession*</span></span> | <span data-ttu-id="ac34a-189">매개 변수는 hello이 사용자는 활성 MFA 세션 hello MFA 세션 관리 tooindicate에서 제공</span><span class="sxs-lookup"><span data-stu-id="ac34a-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="ac34a-190">수집할 수 있는 추가(또는 선택적) 클레임</span><span class="sxs-lookup"><span data-stu-id="ac34a-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="ac34a-191">hello 다음 클레임은 hello 사용자 로부터 수집할 수 있는 추가 클레임 hello 디렉터리에 저장 된 고 hello 토큰에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="ac34a-192">개략적인 설명 대로 하기 전에, 추가 클레임 toothis 목록을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="ac34a-193">클레임 유형</span><span class="sxs-lookup"><span data-stu-id="ac34a-193">Claims type</span></span> | <span data-ttu-id="ac34a-194">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="ac34a-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="ac34a-195">*givenName*</span></span> | <span data-ttu-id="ac34a-196">사용자의 지정된 이름(이름이라고도 함)</span><span class="sxs-lookup"><span data-stu-id="ac34a-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="ac34a-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="ac34a-197">*surname*</span></span> | <span data-ttu-id="ac34a-198">사용자의 성(패밀리 이름 또는 성이라고도 함)</span><span class="sxs-lookup"><span data-stu-id="ac34a-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="ac34a-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="ac34a-199">*Extension_picture*</span></span> | <span data-ttu-id="ac34a-200">소셜에서 사용자의 그림</span><span class="sxs-lookup"><span data-stu-id="ac34a-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="ac34a-201">클레임 변환</span><span class="sxs-lookup"><span data-stu-id="ac34a-201">Claim transformations</span></span>

<span data-ttu-id="ac34a-202">hello 사용 가능한 클레임 변환은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="ac34a-203">클레임 변환</span><span class="sxs-lookup"><span data-stu-id="ac34a-203">Claim transformation</span></span> | <span data-ttu-id="ac34a-204">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="ac34a-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="ac34a-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="ac34a-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="ac34a-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="ac34a-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="ac34a-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="ac34a-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="ac34a-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="ac34a-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="ac34a-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="ac34a-211">콘텐츠 정의</span><span class="sxs-lookup"><span data-stu-id="ac34a-211">Content definitions</span></span>

<span data-ttu-id="ac34a-212">이 섹션에서는 hello에 이미 선언 hello 콘텐츠 정의 설명 *B2C_1A_base* 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="ac34a-213">이 콘텐츠 정의 참조, 재정의 및/또는 hello와 같이 사용자 고유의 정책에서 필요에 따라 확장 취약 toobe *B2C_1A_base_extensions* 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="ac34a-214">클레임 공급자</span><span class="sxs-lookup"><span data-stu-id="ac34a-214">Claims provider</span></span> | <span data-ttu-id="ac34a-215">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="ac34a-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="ac34a-216">*Facebook*</span></span> | |
| <span data-ttu-id="ac34a-217">*로컬 계정 로그인*</span><span class="sxs-lookup"><span data-stu-id="ac34a-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="ac34a-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="ac34a-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="ac34a-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="ac34a-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="ac34a-220">*자체 어설션됨*</span><span class="sxs-lookup"><span data-stu-id="ac34a-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="ac34a-221">*로컬 계정*</span><span class="sxs-lookup"><span data-stu-id="ac34a-221">*Local Account*</span></span> | |
| <span data-ttu-id="ac34a-222">*세션 관리*</span><span class="sxs-lookup"><span data-stu-id="ac34a-222">*Session Management*</span></span> | |
| <span data-ttu-id="ac34a-223">*Trustframework Policy Engine*</span><span class="sxs-lookup"><span data-stu-id="ac34a-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="ac34a-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="ac34a-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="ac34a-225">*토큰 발급자*</span><span class="sxs-lookup"><span data-stu-id="ac34a-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="ac34a-226">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-226">Technical profiles</span></span>

<span data-ttu-id="ac34a-227">이 섹션에서는 hello에 대 한 클레임 공급자 당 이미 선언 되었습니다. hello 기술 프로필을 보여 줍니다. *B2C_1A_base* 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="ac34a-228">이러한 기술 프로필은 더 이상 참조, 재정의 및/또는 hello와 같이 사용자 고유의 정책에서 필요에 따라 확장 취약 toobe *B2C_1A_base_extensions* 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="ac34a-229">Facebook용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="ac34a-230">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-230">Technical profile</span></span> | <span data-ttu-id="ac34a-231">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="ac34a-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="ac34a-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="ac34a-233">로컬 계정 로그인용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="ac34a-234">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-234">Technical profile</span></span> | <span data-ttu-id="ac34a-235">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="ac34a-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="ac34a-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="ac34a-237">Phone Factor용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="ac34a-238">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-238">Technical profile</span></span> | <span data-ttu-id="ac34a-239">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="ac34a-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="ac34a-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="ac34a-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="ac34a-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="ac34a-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="ac34a-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="ac34a-243">Azure Active Directory용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="ac34a-244">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-244">Technical profile</span></span> | <span data-ttu-id="ac34a-245">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="ac34a-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="ac34a-246">*AAD-Common*</span></span> | <span data-ttu-id="ac34a-247">에 의해 포함 되는 기술 프로필 hello 다른 AAD xxx 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="ac34a-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="ac34a-249">소셜 로그인용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="ac34a-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="ac34a-251">소셜 로그인용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="ac34a-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="ac34a-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="ac34a-253">소셜 로그인용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="ac34a-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="ac34a-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="ac34a-255">로컬 계정을 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="ac34a-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="ac34a-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="ac34a-257">로컬 계정을 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="ac34a-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="ac34a-259">objectId를 사용하여 사용자 레코드 업데이트를 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="ac34a-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="ac34a-261">objectId를 사용하여 사용자 레코드 업데이트를 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="ac34a-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="ac34a-263">objectId를 사용하여 사용자 레코드 업데이트를 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="ac34a-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="ac34a-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="ac34a-265">사용자 인증 후 기술 프로필은 tooread 사용 되는 데이터</span><span class="sxs-lookup"><span data-stu-id="ac34a-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="ac34a-266">자체 어설션용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="ac34a-267">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-267">Technical profile</span></span> | <span data-ttu-id="ac34a-268">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="ac34a-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="ac34a-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="ac34a-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="ac34a-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="ac34a-271">로컬 계정용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="ac34a-272">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-272">Technical profile</span></span> | <span data-ttu-id="ac34a-273">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="ac34a-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="ac34a-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="ac34a-275">세션 관리용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="ac34a-276">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-276">Technical profile</span></span> | <span data-ttu-id="ac34a-277">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="ac34a-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="ac34a-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="ac34a-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="ac34a-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="ac34a-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="ac34a-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="ac34a-281">프로필 이름은 기호 간에 사용 되는 toodisambiguate AAD 세션 구성 되 고 이며에 로그인</span><span class="sxs-lookup"><span data-stu-id="ac34a-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="ac34a-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="ac34a-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="ac34a-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="ac34a-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="ac34a-284">Trustframework Policy Engine TechnicalProfiles용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="ac34a-285">Hello에 대 한 기술 프로필이 정의 된 현재 **Trustframework 정책 엔진 TechnicalProfiles** 클레임 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="ac34a-286">토큰 발급자용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="ac34a-287">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="ac34a-287">Technical profile</span></span> | <span data-ttu-id="ac34a-288">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="ac34a-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="ac34a-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="ac34a-290">사용자 경험</span><span class="sxs-lookup"><span data-stu-id="ac34a-290">User journeys</span></span>

<span data-ttu-id="ac34a-291">이 섹션에서는 hello에 이미 선언 hello 사용자 친구를 보여 줍니다. *B2C_1A_base* 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="ac34a-292">이러한 사용자 친구는 더 이상 참조, 재정의 및/또는 hello와 같이 사용자 고유의 정책에서 필요에 따라 확장 취약 toobe *B2C_1A_base_extensions* 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ac34a-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="ac34a-293">사용자 경험</span><span class="sxs-lookup"><span data-stu-id="ac34a-293">User journey</span></span> | <span data-ttu-id="ac34a-294">설명</span><span class="sxs-lookup"><span data-stu-id="ac34a-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="ac34a-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="ac34a-295">*SignUp*</span></span> | |
| <span data-ttu-id="ac34a-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="ac34a-296">*SignIn*</span></span> | |
| <span data-ttu-id="ac34a-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="ac34a-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="ac34a-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="ac34a-298">*EditProfile*</span></span> | |
| <span data-ttu-id="ac34a-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="ac34a-299">*PasswordReset*</span></span> | |
