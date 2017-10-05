---
title: "Azure Active Directory B2C: 시작 팩의 사용자 지정 정책 이해 | Microsoft Docs"
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
ms.openlocfilehash: 9847bcfcc139a769847678c1cca6a8b9c3a30e93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="fdfd6-103">Azure AD B2C 사용자 지정 정책 시작 팩의 사용자 지정 정책 이해</span><span class="sxs-lookup"><span data-stu-id="fdfd6-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="fdfd6-104">이 섹션에서는 **시작 팩**과 함께 제공되고 *B2C_1A_base_extensions 정책*의 상속을 통해 사용자 고유의 정책을 작성하는 데 활용되는 B2C_1A_base 정책의 모든 핵심 요소를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="fdfd6-105">따라서 이미 정의된 클레임 유형, 클레임 변환, 콘텐츠 정의, 기술 프로필이 있는 클레임 공급자 및 핵심 사용자 경험에 특히 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-105">As such, it more particularly focusses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdfd6-106">Microsoft는 이후 제공된 정보에 관해 어떠한 명시적 또는 묵시적 보증도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="fdfd6-107">GA 시간 이전, GA 시간 또는 그 이후에 언제든지 변경 사항을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="fdfd6-108">사용자 고유의 정책과 B2C_1A_base_extensions 정책은 모두 이러한 정의를 재정의하고 필요에 따라 추가 정책을 제공하여 이 상위 정책을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="fdfd6-109">*B2C_1A_base 정책*의 핵심 요소는 클레임 유형, 클레임 변환 및 콘텐츠 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="fdfd6-110">이러한 요소는 *B2C_1A_base_extensions 정책*뿐만 아니라 사용자 고유의 정책에서 쉽게 참조될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="fdfd6-111">클레임 스키마</span><span class="sxs-lookup"><span data-stu-id="fdfd6-111">Claims schemas</span></span>

<span data-ttu-id="fdfd6-112">이 스키마는 다음과 같은 세 가지 섹션으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="fdfd6-113">첫 번째 섹션은 사용자 경험이 제대로 작동하는 데 필요한 최소 클레임을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="fdfd6-114">두 번째 섹션은 다른 클레임 공급자에 전달할 쿼리 문자열 매개 변수 및 기타 특수 매개 변수(특히 인증을 위한 login.microsoftonline.com)에 필요한 클레임을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="fdfd6-115">**이러한 클레임을 수정하지 마세요**.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="fdfd6-116">마지막으로 세 번째 섹션은 사용자로부터 수집하여 디렉터리에 저장하고 로그인 중에 토큰에 전송되는 추가, 선택적인 클레임을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="fdfd6-117">사용자로부터 수집 및/또는 토큰에 전송되는 새 클레임 유형을 이 섹션에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdfd6-118">클레임 스키마는 암호 및 사용자 이름과 같은 특정 스키마에 대한 제한을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="fdfd6-119">보안 프레임워크(TF) 정책은 Azure AD를 다른 클레임 공급자로 처리하며 모든 해당 제한 사항이 프리미엄 정책에서 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the premium policy.</span></span> <span data-ttu-id="fdfd6-120">더 많은 제한 사항을 추가하도록 정책을 수정하거나 사용자 고유의 제한을 포함할 자격 증명 저장소에 대해 다른 클레임 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="fdfd6-121">사용 가능한 클레임 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="fdfd6-122">사용자 경험에 필요한 클레임</span><span class="sxs-lookup"><span data-stu-id="fdfd6-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="fdfd6-123">사용자 경험이 제대로 작동하려면 다음 클레임이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="fdfd6-124">클레임 유형</span><span class="sxs-lookup"><span data-stu-id="fdfd6-124">Claims type</span></span> | <span data-ttu-id="fdfd6-125">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="fdfd6-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-126">*UserId*</span></span> | <span data-ttu-id="fdfd6-127">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="fdfd6-127">Username</span></span> |
| <span data-ttu-id="fdfd6-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-128">*signInName*</span></span> | <span data-ttu-id="fdfd6-129">로그인 이름</span><span class="sxs-lookup"><span data-stu-id="fdfd6-129">Sign in name</span></span> |
| <span data-ttu-id="fdfd6-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-130">*tenantId*</span></span> | <span data-ttu-id="fdfd6-131">Azure AD B2C Premium에서 사용자 개체의 테넌트 식별자(ID)</span><span class="sxs-lookup"><span data-stu-id="fdfd6-131">Tenant identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="fdfd6-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-132">*objectId*</span></span> | <span data-ttu-id="fdfd6-133">Azure AD B2C Premium에서 사용자 개체의 개체 식별자(ID)</span><span class="sxs-lookup"><span data-stu-id="fdfd6-133">Object identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="fdfd6-134">*암호*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-134">*password*</span></span> | <span data-ttu-id="fdfd6-135">암호</span><span class="sxs-lookup"><span data-stu-id="fdfd6-135">Password</span></span> |
| <span data-ttu-id="fdfd6-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-136">*newPassword*</span></span> | |
| <span data-ttu-id="fdfd6-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="fdfd6-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-138">*passwordPolicies*</span></span> | <span data-ttu-id="fdfd6-139">암호 강도, 만료 등을 결정하기 위해 Azure AD B2C Premium에 사용된 암호 정책</span><span class="sxs-lookup"><span data-stu-id="fdfd6-139">Password policies used by Azure AD B2C Premium to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="fdfd6-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-140">*sub*</span></span> | |
| <span data-ttu-id="fdfd6-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="fdfd6-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-142">*identityProvider*</span></span> | |
| <span data-ttu-id="fdfd6-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-143">*displayName*</span></span> | |
| <span data-ttu-id="fdfd6-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="fdfd6-145">사용자의 전화 번호</span><span class="sxs-lookup"><span data-stu-id="fdfd6-145">User's telephone number</span></span> |
| <span data-ttu-id="fdfd6-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="fdfd6-147">*email*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-147">*email*</span></span> | <span data-ttu-id="fdfd6-148">사용자에게 연락하는 데 사용할 수 있는 이메일 주소</span><span class="sxs-lookup"><span data-stu-id="fdfd6-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="fdfd6-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="fdfd6-150">사용자가 로그인에 사용할 수 있는 이메일 주소</span><span class="sxs-lookup"><span data-stu-id="fdfd6-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="fdfd6-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-151">*otherMails*</span></span> | <span data-ttu-id="fdfd6-152">사용자에게 연결하는 데 사용할 수 있는 이메일 주소</span><span class="sxs-lookup"><span data-stu-id="fdfd6-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="fdfd6-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-153">*userPrincipalName*</span></span> | <span data-ttu-id="fdfd6-154">Azure AD B2C Premium에 저장된 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="fdfd6-154">Username as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="fdfd6-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-155">*upnUserName*</span></span> | <span data-ttu-id="fdfd6-156">사용자 계정 이름을 만들기 위한 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="fdfd6-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="fdfd6-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-157">*mailNickName*</span></span> | <span data-ttu-id="fdfd6-158">Azure AD B2C Premium에 저장된 사용자의 메일 별명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-158">User's mail nick name as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="fdfd6-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-159">*newUser*</span></span> | |
| <span data-ttu-id="fdfd6-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="fdfd6-161">사용자로부터 특성을 수집할지 여부를 지정하는 클레임</span><span class="sxs-lookup"><span data-stu-id="fdfd6-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="fdfd6-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="fdfd6-163">사용자로부터 새 전화 번호를 수집할지 여부를 지정하는 클레임</span><span class="sxs-lookup"><span data-stu-id="fdfd6-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="fdfd6-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-164">*authenticationSource*</span></span> | <span data-ttu-id="fdfd6-165">사용자가 소셜 ID 공급자, login.microsoftonline.com 또는 로컬 계정에서 인증되었는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="fdfd6-166">쿼리 문자열 매개 변수 및 기타 특수 매개 변수에 필요한 클레임</span><span class="sxs-lookup"><span data-stu-id="fdfd6-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="fdfd6-167">특수 매개 변수(일부 쿼리 문자열 매개 변수 포함)에서 다른 클레임 공급자로 전달하는 데 다음 클레임이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="fdfd6-168">클레임 유형</span><span class="sxs-lookup"><span data-stu-id="fdfd6-168">Claims type</span></span> | <span data-ttu-id="fdfd6-169">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="fdfd6-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-170">*nux*</span></span> | <span data-ttu-id="fdfd6-171">로컬 계정 인증을 위해 login.microsoftonline.com에 전달하는 특수 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="fdfd6-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-172">*nca*</span></span> | <span data-ttu-id="fdfd6-173">로컬 계정 인증을 위해 login.microsoftonline.com에 전달하는 특수 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="fdfd6-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-174">*prompt*</span></span> | <span data-ttu-id="fdfd6-175">로컬 계정 인증을 위해 login.microsoftonline.com에 전달하는 특수 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="fdfd6-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-176">*mkt*</span></span> | <span data-ttu-id="fdfd6-177">로컬 계정 인증을 위해 login.microsoftonline.com에 전달하는 특수 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="fdfd6-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-178">*lc*</span></span> | <span data-ttu-id="fdfd6-179">로컬 계정 인증을 위해 login.microsoftonline.com에 전달하는 특수 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="fdfd6-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-180">*grant_type*</span></span> | <span data-ttu-id="fdfd6-181">로컬 계정 인증을 위해 login.microsoftonline.com에 전달하는 특수 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="fdfd6-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-182">*scope*</span></span> | <span data-ttu-id="fdfd6-183">로컬 계정 인증을 위해 login.microsoftonline.com에 전달하는 특수 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="fdfd6-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-184">*client_id*</span></span> | <span data-ttu-id="fdfd6-185">로컬 계정 인증을 위해 login.microsoftonline.com에 전달하는 특수 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="fdfd6-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-186">*objectIdFromSession*</span></span> | <span data-ttu-id="fdfd6-187">개체 ID가 SSO 세션에서 검색되었음을 나타내기 위해 기본 세션 관리 공급자가 제공한 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-187">Parameter provided by the default session management provider to indicate that the object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="fdfd6-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-188">*isActiveMFASession*</span></span> | <span data-ttu-id="fdfd6-189">사용자가 활성 MFA 세션을 포함하고 있음을 나타내기 위해 MFA 세션 관리에서 제공한 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fdfd6-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="fdfd6-190">수집할 수 있는 추가(또는 선택적) 클레임</span><span class="sxs-lookup"><span data-stu-id="fdfd6-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="fdfd6-191">다음 클레임은 사용자로부터 수집하여 디렉터리에 저장하고 토큰에 전송되는 추가 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="fdfd6-192">전에 설명한 바와 같이 추가 클레임은 이 목록에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="fdfd6-193">클레임 유형</span><span class="sxs-lookup"><span data-stu-id="fdfd6-193">Claims type</span></span> | <span data-ttu-id="fdfd6-194">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="fdfd6-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-195">*givenName*</span></span> | <span data-ttu-id="fdfd6-196">사용자의 지정된 이름(이름이라고도 함)</span><span class="sxs-lookup"><span data-stu-id="fdfd6-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="fdfd6-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-197">*surname*</span></span> | <span data-ttu-id="fdfd6-198">사용자의 성(패밀리 이름 또는 성이라고도 함)</span><span class="sxs-lookup"><span data-stu-id="fdfd6-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="fdfd6-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-199">*Extension_picture*</span></span> | <span data-ttu-id="fdfd6-200">소셜에서 사용자의 그림</span><span class="sxs-lookup"><span data-stu-id="fdfd6-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="fdfd6-201">클레임 변환</span><span class="sxs-lookup"><span data-stu-id="fdfd6-201">Claim transformations</span></span>

<span data-ttu-id="fdfd6-202">사용 가능한 클레임 변환은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="fdfd6-203">클레임 변환</span><span class="sxs-lookup"><span data-stu-id="fdfd6-203">Claim transformation</span></span> | <span data-ttu-id="fdfd6-204">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="fdfd6-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="fdfd6-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="fdfd6-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="fdfd6-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="fdfd6-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="fdfd6-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="fdfd6-211">콘텐츠 정의</span><span class="sxs-lookup"><span data-stu-id="fdfd6-211">Content definitions</span></span>

<span data-ttu-id="fdfd6-212">이 섹션에서는 *B2C_1A_base* 정책에 이미 선언된 콘텐츠 정의를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="fdfd6-213">이러한 콘텐츠 정의는 *B2C_1A_base_extensions* 정책뿐만 아니라 사용자 고유의 정책에서 필요에 따라 쉽게 참조, 재정의 및/또는 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="fdfd6-214">클레임 공급자</span><span class="sxs-lookup"><span data-stu-id="fdfd6-214">Claims provider</span></span> | <span data-ttu-id="fdfd6-215">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="fdfd6-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-216">*Facebook*</span></span> | |
| <span data-ttu-id="fdfd6-217">*로컬 계정 로그인*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="fdfd6-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="fdfd6-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="fdfd6-220">*자체 어설션됨*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="fdfd6-221">*로컬 계정*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-221">*Local Account*</span></span> | |
| <span data-ttu-id="fdfd6-222">*세션 관리*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-222">*Session Management*</span></span> | |
| <span data-ttu-id="fdfd6-223">*Trustframework Policy Engine*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="fdfd6-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="fdfd6-225">*토큰 발급자*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="fdfd6-226">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-226">Technical profiles</span></span>

<span data-ttu-id="fdfd6-227">이 섹션에서는 *B2C_1A_base* 정책에서 클레임 공급자마다 이미 선언된 기술 프로필을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="fdfd6-228">이러한 기술 프로필은 *B2C_1A_base_extensions* 정책뿐만 아니라 사용자 고유의 정책에서 필요에 따라 쉽게 참조, 재정의 및/또는 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="fdfd6-229">Facebook용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="fdfd6-230">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-230">Technical profile</span></span> | <span data-ttu-id="fdfd6-231">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="fdfd6-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="fdfd6-233">로컬 계정 로그인용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="fdfd6-234">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-234">Technical profile</span></span> | <span data-ttu-id="fdfd6-235">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="fdfd6-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="fdfd6-237">Phone Factor용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="fdfd6-238">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-238">Technical profile</span></span> | <span data-ttu-id="fdfd6-239">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="fdfd6-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="fdfd6-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="fdfd6-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="fdfd6-243">Azure Active Directory용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="fdfd6-244">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-244">Technical profile</span></span> | <span data-ttu-id="fdfd6-245">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="fdfd6-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-246">*AAD-Common*</span></span> | <span data-ttu-id="fdfd6-247">다른 AAD-xxx 기술 프로필에 포함된 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="fdfd6-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="fdfd6-249">소셜 로그인용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="fdfd6-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="fdfd6-251">소셜 로그인용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="fdfd6-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="fdfd6-253">소셜 로그인용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="fdfd6-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="fdfd6-255">로컬 계정을 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="fdfd6-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="fdfd6-257">로컬 계정을 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="fdfd6-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="fdfd6-259">objectId를 사용하여 사용자 레코드 업데이트를 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="fdfd6-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="fdfd6-261">objectId를 사용하여 사용자 레코드 업데이트를 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="fdfd6-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="fdfd6-263">objectId를 사용하여 사용자 레코드 업데이트를 위한 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="fdfd6-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="fdfd6-265">사용자 인증 후 데이터를 읽는 데 사용되는 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="fdfd6-266">자체 어설션용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="fdfd6-267">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-267">Technical profile</span></span> | <span data-ttu-id="fdfd6-268">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="fdfd6-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="fdfd6-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="fdfd6-271">로컬 계정용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="fdfd6-272">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-272">Technical profile</span></span> | <span data-ttu-id="fdfd6-273">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="fdfd6-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="fdfd6-275">세션 관리용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="fdfd6-276">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-276">Technical profile</span></span> | <span data-ttu-id="fdfd6-277">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="fdfd6-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="fdfd6-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="fdfd6-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="fdfd6-281">프로필 이름은 등록 및 로그인 간에 AAD 세션을 구분하는 데 사용됨</span><span class="sxs-lookup"><span data-stu-id="fdfd6-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="fdfd6-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="fdfd6-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="fdfd6-284">Trustframework Policy Engine TechnicalProfiles용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="fdfd6-285">현재는 **Trustframework Policy Engine TechnicalProfiles** 클레임 공급자에 대해 정의된 기술 프로필이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="fdfd6-286">토큰 발급자용 기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="fdfd6-287">기술 프로필</span><span class="sxs-lookup"><span data-stu-id="fdfd6-287">Technical profile</span></span> | <span data-ttu-id="fdfd6-288">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="fdfd6-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="fdfd6-290">사용자 경험</span><span class="sxs-lookup"><span data-stu-id="fdfd6-290">User journeys</span></span>

<span data-ttu-id="fdfd6-291">이 섹션에서는 *B2C_1A_base* 정책에 이미 선언된 사용자 경험을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="fdfd6-292">이러한 사용자 경험은 *B2C_1A_base_extensions* 정책뿐만 아니라 사용자 고유의 정책에서 필요에 따라 쉽게 참조, 재정의 및/또는 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdfd6-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="fdfd6-293">사용자 경험</span><span class="sxs-lookup"><span data-stu-id="fdfd6-293">User journey</span></span> | <span data-ttu-id="fdfd6-294">설명</span><span class="sxs-lookup"><span data-stu-id="fdfd6-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="fdfd6-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-295">*SignUp*</span></span> | |
| <span data-ttu-id="fdfd6-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-296">*SignIn*</span></span> | |
| <span data-ttu-id="fdfd6-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="fdfd6-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-298">*EditProfile*</span></span> | |
| <span data-ttu-id="fdfd6-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="fdfd6-299">*PasswordReset*</span></span> | |
