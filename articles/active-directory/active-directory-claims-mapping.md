---
title: "Azure Active Directory의 클레임 매핑(공개 미리 보기) | Microsoft Docs"
description: "이 페이지에서는 Azure Active Directory 클레임 매핑을 설명합니다."
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a><span data-ttu-id="69091-103">Azure Active Directory의 클레임 매핑(공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="69091-103">Claims mapping in Azure Active Directory (public preview)</span></span>

>[!NOTE]
><span data-ttu-id="69091-104">이 기능은 대체 하 고 hello 대체 [사용자 지정 클레임](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) 현재 hello 포털을 통해 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-104">This feature replaces and supersedes hello [claims customization](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) offered through hello portal today.</span></span> <span data-ttu-id="69091-105">Hello 포털을 사용 하 여 클레임을 사용자 지정 하는 경우 또한 toohello 그래프/PowerShell 메서드이 문서에에서 자세히 설명이 hello에 동일한 응용 프로그램, 해당 응용 프로그램에서 무시 hello 포털에서 hello 구성 용으로 발급 된 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-105">If you customize claims using hello portal in addition toohello Graph/PowerShell method detailed in this document on hello same application, tokens issued for that application will ignore hello configuration in hello portal.</span></span>
<span data-ttu-id="69091-106">이 문서에에서 자세히 설명 하는 hello 메서드를 통해 구성이 hello 포털에 반영 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-106">Configurations made through hello methods detailed in this document will not be reflected in hello portal.</span></span>

<span data-ttu-id="69091-107">이 기능은 테 넌 트에 특정 응용 프로그램에 대 한 토큰에 포함 된 테 넌 트 관리자 toocustomize hello 클레임으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69091-107">This feature is used by tenant admins toocustomize hello claims emitted in tokens for a specific application in their tenant.</span></span> <span data-ttu-id="69091-108">다음과 같은 경우 클레임 매핑 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-108">You can use claims mapping policies to:</span></span>

- <span data-ttu-id="69091-109">토큰에 포함할 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-109">Select which claims are included in tokens.</span></span>
- <span data-ttu-id="69091-110">아직 존재하지 않는 클레임 형식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69091-110">Create claim types that do not already exist.</span></span>
- <span data-ttu-id="69091-111">선택 하거나 특정 클레임에 포함 된 데이터의 hello 원본을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-111">Choose or change hello source of data emitted in specific claims.</span></span>

>[!NOTE]
><span data-ttu-id="69091-112">이 기능은 현재 공개 미리 보기로 제공되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-112">This capability currently is in public preview.</span></span> <span data-ttu-id="69091-113">Toorevert 준비 하거나 변경 내용을 모두 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-113">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="69091-114">hello 기능은 공개 미리 보기 기간 동안 모든 Azure Active Directory (Azure AD) 구독에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-114">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="69091-115">그러나 hello 기능이 일반 공급 되 면 hello 기능의 일부 측면 Azure Active Directory premium 구독에 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-115">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>

## <a name="claims-mapping-policy-type"></a><span data-ttu-id="69091-116">클레임 매핑 정책 유형</span><span class="sxs-lookup"><span data-stu-id="69091-116">Claims mapping policy type</span></span>
<span data-ttu-id="69091-117">Azure AD에서 **정책** 개체는 조직에 있는 개별 응용 프로그램 또는 모든 응용 프로그램에 적용되는 규칙 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69091-117">In Azure AD, a **Policy** object represents a set of rules enforced on individual applications, or on all applications in an organization.</span></span> <span data-ttu-id="69091-118">각 정책 종류가 되는 속성 집합이 있는 고유한 구조는 다음 tooobjects toowhich 할당을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-118">Each type of policy has a unique structure, with a set of properties that are then applied tooobjects toowhich they are assigned.</span></span>

<span data-ttu-id="69091-119">A 클레임의 형식인 정책 매핑 **정책** hello를 수정 하는 개체는 특정 응용 프로그램에 발급 한 토큰에 포함 된 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-119">A claims mapping policy is a type of **Policy** object that modifies hello claims emitted in tokens issued for specific applications.</span></span>

## <a name="claim-sets"></a><span data-ttu-id="69091-120">클레임 집합</span><span class="sxs-lookup"><span data-stu-id="69091-120">Claim sets</span></span>
<span data-ttu-id="69091-121">토큰에 사용되는 시기와 방법을 정의하는 특정 클레임 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-121">There are certain sets of claims that define how and when they are used in tokens.</span></span>

### <a name="core-claim-set"></a><span data-ttu-id="69091-122">핵심 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="69091-122">Core claim set</span></span>
<span data-ttu-id="69091-123">Hello 코어에서 클레임 정책에 관계 없이 모든 토큰에 있는 집합을 요청 하십시오.</span><span class="sxs-lookup"><span data-stu-id="69091-123">Claims in hello core claim set are present in every token, regardless of policy.</span></span> <span data-ttu-id="69091-124">또한 이러한 클레임은 제한된 것으로 간주되며 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-124">These claims are also considered restricted, and cannot be modified.</span></span>

### <a name="basic-claim-set"></a><span data-ttu-id="69091-125">기본 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="69091-125">Basic claim set</span></span>
<span data-ttu-id="69091-126">hello 기본 클레임 집합에는 토큰 (더하기 toohello 코어 클레임 집합)에 대 한 기본적으로 발생 하는 hello 클레임 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69091-126">hello basic claim set includes hello claims that are emitted by default for tokens (in addition toohello core claim set).</span></span> <span data-ttu-id="69091-127">이러한 클레임을 생략 하면 또는 정책 매핑 hello 클레임을 사용 하 여 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-127">These claims can be omitted or modified by using hello claims mapping policies.</span></span>

### <a name="restricted-claim-set"></a><span data-ttu-id="69091-128">제한된 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="69091-128">Restricted claim set</span></span>
<span data-ttu-id="69091-129">정책을 사용하여 제한된 클레임을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-129">Restricted claims cannot be modified by using policy.</span></span> <span data-ttu-id="69091-130">hello 데이터 소스를 변경할 수 없으며, 및 이러한 클레임을 생성 하는 경우 변환이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69091-130">hello data source cannot be changed, and no transformation is applied when generating these claims.</span></span>

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a><span data-ttu-id="69091-131">표 1: JWT(JSON Web Token) 제한된 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="69091-131">Table 1: JSON Web Token (JWT) restricted claim set</span></span>
|<span data-ttu-id="69091-132">클레임 형식(이름)</span><span class="sxs-lookup"><span data-stu-id="69091-132">Claim type (name)</span></span>|
| ----- |
|<span data-ttu-id="69091-133">_claim_names</span><span class="sxs-lookup"><span data-stu-id="69091-133">_claim_names</span></span>|
|<span data-ttu-id="69091-134">_claim_sources</span><span class="sxs-lookup"><span data-stu-id="69091-134">_claim_sources</span></span>|
|<span data-ttu-id="69091-135">access_token</span><span class="sxs-lookup"><span data-stu-id="69091-135">access_token</span></span>|
|<span data-ttu-id="69091-136">account_type</span><span class="sxs-lookup"><span data-stu-id="69091-136">account_type</span></span>|
|<span data-ttu-id="69091-137">acr</span><span class="sxs-lookup"><span data-stu-id="69091-137">acr</span></span>|
|<span data-ttu-id="69091-138">actor</span><span class="sxs-lookup"><span data-stu-id="69091-138">actor</span></span>|
|<span data-ttu-id="69091-139">actortoken</span><span class="sxs-lookup"><span data-stu-id="69091-139">actortoken</span></span>|
|<span data-ttu-id="69091-140">aio</span><span class="sxs-lookup"><span data-stu-id="69091-140">aio</span></span>|
|<span data-ttu-id="69091-141">altsecid</span><span class="sxs-lookup"><span data-stu-id="69091-141">altsecid</span></span>|
|<span data-ttu-id="69091-142">amr</span><span class="sxs-lookup"><span data-stu-id="69091-142">amr</span></span>|
|<span data-ttu-id="69091-143">app_chain</span><span class="sxs-lookup"><span data-stu-id="69091-143">app_chain</span></span>|
|<span data-ttu-id="69091-144">app_displayname</span><span class="sxs-lookup"><span data-stu-id="69091-144">app_displayname</span></span>|
|<span data-ttu-id="69091-145">app_res</span><span class="sxs-lookup"><span data-stu-id="69091-145">app_res</span></span>|
|<span data-ttu-id="69091-146">appctx</span><span class="sxs-lookup"><span data-stu-id="69091-146">appctx</span></span>|
|<span data-ttu-id="69091-147">appctxsender</span><span class="sxs-lookup"><span data-stu-id="69091-147">appctxsender</span></span>|
|<span data-ttu-id="69091-148">appId</span><span class="sxs-lookup"><span data-stu-id="69091-148">appid</span></span>|
|<span data-ttu-id="69091-149">appidacr</span><span class="sxs-lookup"><span data-stu-id="69091-149">appidacr</span></span>|
|<span data-ttu-id="69091-150">어설션</span><span class="sxs-lookup"><span data-stu-id="69091-150">assertion</span></span>|
|<span data-ttu-id="69091-151">at_hash</span><span class="sxs-lookup"><span data-stu-id="69091-151">at_hash</span></span>|
|<span data-ttu-id="69091-152">aud</span><span class="sxs-lookup"><span data-stu-id="69091-152">aud</span></span>|
|<span data-ttu-id="69091-153">auth_data</span><span class="sxs-lookup"><span data-stu-id="69091-153">auth_data</span></span>|
|<span data-ttu-id="69091-154">auth_time</span><span class="sxs-lookup"><span data-stu-id="69091-154">auth_time</span></span>|
|<span data-ttu-id="69091-155">authorization_code</span><span class="sxs-lookup"><span data-stu-id="69091-155">authorization_code</span></span>|
|<span data-ttu-id="69091-156">azp</span><span class="sxs-lookup"><span data-stu-id="69091-156">azp</span></span>|
|<span data-ttu-id="69091-157">azpacr</span><span class="sxs-lookup"><span data-stu-id="69091-157">azpacr</span></span>|
|<span data-ttu-id="69091-158">c_hash</span><span class="sxs-lookup"><span data-stu-id="69091-158">c_hash</span></span>|
|<span data-ttu-id="69091-159">ca_enf</span><span class="sxs-lookup"><span data-stu-id="69091-159">ca_enf</span></span>|
|<span data-ttu-id="69091-160">cc</span><span class="sxs-lookup"><span data-stu-id="69091-160">cc</span></span>|
|<span data-ttu-id="69091-161">cert_token_use</span><span class="sxs-lookup"><span data-stu-id="69091-161">cert_token_use</span></span>|
|<span data-ttu-id="69091-162">client_id</span><span class="sxs-lookup"><span data-stu-id="69091-162">client_id</span></span>|
|<span data-ttu-id="69091-163">cloud_graph_host_name</span><span class="sxs-lookup"><span data-stu-id="69091-163">cloud_graph_host_name</span></span>|
|<span data-ttu-id="69091-164">cloud_instance_name</span><span class="sxs-lookup"><span data-stu-id="69091-164">cloud_instance_name</span></span>|
|<span data-ttu-id="69091-165">cnf</span><span class="sxs-lookup"><span data-stu-id="69091-165">cnf</span></span>|
|<span data-ttu-id="69091-166">코드</span><span class="sxs-lookup"><span data-stu-id="69091-166">code</span></span>|
|<span data-ttu-id="69091-167">controls</span><span class="sxs-lookup"><span data-stu-id="69091-167">controls</span></span>|
|<span data-ttu-id="69091-168">credential_keys</span><span class="sxs-lookup"><span data-stu-id="69091-168">credential_keys</span></span>|
|<span data-ttu-id="69091-169">csr</span><span class="sxs-lookup"><span data-stu-id="69091-169">csr</span></span>|
|<span data-ttu-id="69091-170">csr_type</span><span class="sxs-lookup"><span data-stu-id="69091-170">csr_type</span></span>|
|<span data-ttu-id="69091-171">deviceId</span><span class="sxs-lookup"><span data-stu-id="69091-171">deviceid</span></span>|
|<span data-ttu-id="69091-172">dns_names</span><span class="sxs-lookup"><span data-stu-id="69091-172">dns_names</span></span>|
|<span data-ttu-id="69091-173">domain_dns_name</span><span class="sxs-lookup"><span data-stu-id="69091-173">domain_dns_name</span></span>|
|<span data-ttu-id="69091-174">domain_netbios_name</span><span class="sxs-lookup"><span data-stu-id="69091-174">domain_netbios_name</span></span>|
|<span data-ttu-id="69091-175">e_exp</span><span class="sxs-lookup"><span data-stu-id="69091-175">e_exp</span></span>|
|<span data-ttu-id="69091-176">email</span><span class="sxs-lookup"><span data-stu-id="69091-176">email</span></span>|
|<span data-ttu-id="69091-177">endpoint</span><span class="sxs-lookup"><span data-stu-id="69091-177">endpoint</span></span>|
|<span data-ttu-id="69091-178">enfpolids</span><span class="sxs-lookup"><span data-stu-id="69091-178">enfpolids</span></span>|
|<span data-ttu-id="69091-179">exp</span><span class="sxs-lookup"><span data-stu-id="69091-179">exp</span></span>|
|<span data-ttu-id="69091-180">expires_on</span><span class="sxs-lookup"><span data-stu-id="69091-180">expires_on</span></span>|
|<span data-ttu-id="69091-181">grant_type</span><span class="sxs-lookup"><span data-stu-id="69091-181">grant_type</span></span>|
|<span data-ttu-id="69091-182">graph</span><span class="sxs-lookup"><span data-stu-id="69091-182">graph</span></span>|
|<span data-ttu-id="69091-183">group_sids</span><span class="sxs-lookup"><span data-stu-id="69091-183">group_sids</span></span>|
|<span data-ttu-id="69091-184">groups</span><span class="sxs-lookup"><span data-stu-id="69091-184">groups</span></span>|
|<span data-ttu-id="69091-185">hasgroups</span><span class="sxs-lookup"><span data-stu-id="69091-185">hasgroups</span></span>|
|<span data-ttu-id="69091-186">hash_alg</span><span class="sxs-lookup"><span data-stu-id="69091-186">hash_alg</span></span>|
|<span data-ttu-id="69091-187">home_oid</span><span class="sxs-lookup"><span data-stu-id="69091-187">home_oid</span></span>|
|<span data-ttu-id="69091-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="69091-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span>|
|<span data-ttu-id="69091-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="69091-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span>|
|<span data-ttu-id="69091-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="69091-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span>|
|<span data-ttu-id="69091-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="69091-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span>|
|<span data-ttu-id="69091-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="69091-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span>|
|<span data-ttu-id="69091-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name</span><span class="sxs-lookup"><span data-stu-id="69091-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name</span></span>|
|<span data-ttu-id="69091-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier</span><span class="sxs-lookup"><span data-stu-id="69091-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier</span></span>|
|<span data-ttu-id="69091-195">iat</span><span class="sxs-lookup"><span data-stu-id="69091-195">iat</span></span>|
|<span data-ttu-id="69091-196">identityprovider</span><span class="sxs-lookup"><span data-stu-id="69091-196">identityprovider</span></span>|
|<span data-ttu-id="69091-197">idp</span><span class="sxs-lookup"><span data-stu-id="69091-197">idp</span></span>|
|<span data-ttu-id="69091-198">in_corp</span><span class="sxs-lookup"><span data-stu-id="69091-198">in_corp</span></span>|
|<span data-ttu-id="69091-199">instance</span><span class="sxs-lookup"><span data-stu-id="69091-199">instance</span></span>|
|<span data-ttu-id="69091-200">ipaddr</span><span class="sxs-lookup"><span data-stu-id="69091-200">ipaddr</span></span>|
|<span data-ttu-id="69091-201">isbrowserhostedapp</span><span class="sxs-lookup"><span data-stu-id="69091-201">isbrowserhostedapp</span></span>|
|<span data-ttu-id="69091-202">iss</span><span class="sxs-lookup"><span data-stu-id="69091-202">iss</span></span>|
|<span data-ttu-id="69091-203">jwk</span><span class="sxs-lookup"><span data-stu-id="69091-203">jwk</span></span>|
|<span data-ttu-id="69091-204">key_id</span><span class="sxs-lookup"><span data-stu-id="69091-204">key_id</span></span>|
|<span data-ttu-id="69091-205">key_type</span><span class="sxs-lookup"><span data-stu-id="69091-205">key_type</span></span>|
|<span data-ttu-id="69091-206">mam_compliance_url</span><span class="sxs-lookup"><span data-stu-id="69091-206">mam_compliance_url</span></span>|
|<span data-ttu-id="69091-207">mam_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="69091-207">mam_enrollment_url</span></span>|
|<span data-ttu-id="69091-208">mam_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="69091-208">mam_terms_of_use_url</span></span>|
|<span data-ttu-id="69091-209">mdm_compliance_url</span><span class="sxs-lookup"><span data-stu-id="69091-209">mdm_compliance_url</span></span>|
|<span data-ttu-id="69091-210">mdm_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="69091-210">mdm_enrollment_url</span></span>|
|<span data-ttu-id="69091-211">mdm_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="69091-211">mdm_terms_of_use_url</span></span>|
|<span data-ttu-id="69091-212">nameid</span><span class="sxs-lookup"><span data-stu-id="69091-212">nameid</span></span>|
|<span data-ttu-id="69091-213">nbf</span><span class="sxs-lookup"><span data-stu-id="69091-213">nbf</span></span>|
|<span data-ttu-id="69091-214">netbios_name</span><span class="sxs-lookup"><span data-stu-id="69091-214">netbios_name</span></span>|
|<span data-ttu-id="69091-215">nonce</span><span class="sxs-lookup"><span data-stu-id="69091-215">nonce</span></span>|
|<span data-ttu-id="69091-216">oid</span><span class="sxs-lookup"><span data-stu-id="69091-216">oid</span></span>|
|<span data-ttu-id="69091-217">on_prem_id</span><span class="sxs-lookup"><span data-stu-id="69091-217">on_prem_id</span></span>|
|<span data-ttu-id="69091-218">onprem_sam_account_name</span><span class="sxs-lookup"><span data-stu-id="69091-218">onprem_sam_account_name</span></span>|
|<span data-ttu-id="69091-219">onprem_sid</span><span class="sxs-lookup"><span data-stu-id="69091-219">onprem_sid</span></span>|
|<span data-ttu-id="69091-220">openid2_id</span><span class="sxs-lookup"><span data-stu-id="69091-220">openid2_id</span></span>|
|<span data-ttu-id="69091-221">password</span><span class="sxs-lookup"><span data-stu-id="69091-221">password</span></span>|
|<span data-ttu-id="69091-222">platf</span><span class="sxs-lookup"><span data-stu-id="69091-222">platf</span></span>|
|<span data-ttu-id="69091-223">polids</span><span class="sxs-lookup"><span data-stu-id="69091-223">polids</span></span>|
|<span data-ttu-id="69091-224">pop_jwk</span><span class="sxs-lookup"><span data-stu-id="69091-224">pop_jwk</span></span>|
|<span data-ttu-id="69091-225">preferred_username</span><span class="sxs-lookup"><span data-stu-id="69091-225">preferred_username</span></span>|
|<span data-ttu-id="69091-226">previous_refresh_token</span><span class="sxs-lookup"><span data-stu-id="69091-226">previous_refresh_token</span></span>|
|<span data-ttu-id="69091-227">primary_sid</span><span class="sxs-lookup"><span data-stu-id="69091-227">primary_sid</span></span>|
|<span data-ttu-id="69091-228">puid</span><span class="sxs-lookup"><span data-stu-id="69091-228">puid</span></span>|
|<span data-ttu-id="69091-229">pwd_exp</span><span class="sxs-lookup"><span data-stu-id="69091-229">pwd_exp</span></span>|
|<span data-ttu-id="69091-230">pwd_url</span><span class="sxs-lookup"><span data-stu-id="69091-230">pwd_url</span></span>|
|<span data-ttu-id="69091-231">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="69091-231">redirect_uri</span></span>|
|<span data-ttu-id="69091-232">refresh_token</span><span class="sxs-lookup"><span data-stu-id="69091-232">refresh_token</span></span>|
|<span data-ttu-id="69091-233">refreshtoken</span><span class="sxs-lookup"><span data-stu-id="69091-233">refreshtoken</span></span>|
|<span data-ttu-id="69091-234">request_nonce</span><span class="sxs-lookup"><span data-stu-id="69091-234">request_nonce</span></span>|
|<span data-ttu-id="69091-235">resource</span><span class="sxs-lookup"><span data-stu-id="69091-235">resource</span></span>|
|<span data-ttu-id="69091-236">role</span><span class="sxs-lookup"><span data-stu-id="69091-236">role</span></span>|
|<span data-ttu-id="69091-237">roles</span><span class="sxs-lookup"><span data-stu-id="69091-237">roles</span></span>|
|<span data-ttu-id="69091-238">scope</span><span class="sxs-lookup"><span data-stu-id="69091-238">scope</span></span>|
|<span data-ttu-id="69091-239">scp</span><span class="sxs-lookup"><span data-stu-id="69091-239">scp</span></span>|
|<span data-ttu-id="69091-240">sid</span><span class="sxs-lookup"><span data-stu-id="69091-240">sid</span></span>|
|<span data-ttu-id="69091-241">signature</span><span class="sxs-lookup"><span data-stu-id="69091-241">signature</span></span>|
|<span data-ttu-id="69091-242">signin_state</span><span class="sxs-lookup"><span data-stu-id="69091-242">signin_state</span></span>|
|<span data-ttu-id="69091-243">src1</span><span class="sxs-lookup"><span data-stu-id="69091-243">src1</span></span>|
|<span data-ttu-id="69091-244">src2</span><span class="sxs-lookup"><span data-stu-id="69091-244">src2</span></span>|
|<span data-ttu-id="69091-245">sub</span><span class="sxs-lookup"><span data-stu-id="69091-245">sub</span></span>|
|<span data-ttu-id="69091-246">tbid</span><span class="sxs-lookup"><span data-stu-id="69091-246">tbid</span></span>|
|<span data-ttu-id="69091-247">tenant_display_name</span><span class="sxs-lookup"><span data-stu-id="69091-247">tenant_display_name</span></span>|
|<span data-ttu-id="69091-248">tenant_region_scope</span><span class="sxs-lookup"><span data-stu-id="69091-248">tenant_region_scope</span></span>|
|<span data-ttu-id="69091-249">thumbnail_photo</span><span class="sxs-lookup"><span data-stu-id="69091-249">thumbnail_photo</span></span>|
|<span data-ttu-id="69091-250">tid</span><span class="sxs-lookup"><span data-stu-id="69091-250">tid</span></span>|
|<span data-ttu-id="69091-251">tokenAutologonEnabled</span><span class="sxs-lookup"><span data-stu-id="69091-251">tokenAutologonEnabled</span></span>|
|<span data-ttu-id="69091-252">trustedfordelegation</span><span class="sxs-lookup"><span data-stu-id="69091-252">trustedfordelegation</span></span>|
|<span data-ttu-id="69091-253">unique_name</span><span class="sxs-lookup"><span data-stu-id="69091-253">unique_name</span></span>|
|<span data-ttu-id="69091-254">upn</span><span class="sxs-lookup"><span data-stu-id="69091-254">upn</span></span>|
|<span data-ttu-id="69091-255">user_setting_sync_url</span><span class="sxs-lookup"><span data-stu-id="69091-255">user_setting_sync_url</span></span>|
|<span data-ttu-id="69091-256">username</span><span class="sxs-lookup"><span data-stu-id="69091-256">username</span></span>|
|<span data-ttu-id="69091-257">uti</span><span class="sxs-lookup"><span data-stu-id="69091-257">uti</span></span>|
|<span data-ttu-id="69091-258">ver</span><span class="sxs-lookup"><span data-stu-id="69091-258">ver</span></span>|
|<span data-ttu-id="69091-259">verified_primary_email</span><span class="sxs-lookup"><span data-stu-id="69091-259">verified_primary_email</span></span>|
|<span data-ttu-id="69091-260">verified_secondary_email</span><span class="sxs-lookup"><span data-stu-id="69091-260">verified_secondary_email</span></span>|
|<span data-ttu-id="69091-261">wids</span><span class="sxs-lookup"><span data-stu-id="69091-261">wids</span></span>|
|<span data-ttu-id="69091-262">win_ver</span><span class="sxs-lookup"><span data-stu-id="69091-262">win_ver</span></span>|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a><span data-ttu-id="69091-263">표 2: SAML(Security Assertion Markup Language) 제한된 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="69091-263">Table 2: Security Assertion Markup Language (SAML) restricted claim set</span></span>
|<span data-ttu-id="69091-264">클레임 형식(URI)</span><span class="sxs-lookup"><span data-stu-id="69091-264">Claim type (URI)</span></span>|
| ----- |
|<span data-ttu-id="69091-265">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="69091-265">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span>|
|<span data-ttu-id="69091-266">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="69091-266">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span>|
|<span data-ttu-id="69091-267">http://schemas.microsoft.com/identity/claims/accesstoken</span><span class="sxs-lookup"><span data-stu-id="69091-267">http://schemas.microsoft.com/identity/claims/accesstoken</span></span>|
|<span data-ttu-id="69091-268">http://schemas.microsoft.com/identity/claims/openid2_id</span><span class="sxs-lookup"><span data-stu-id="69091-268">http://schemas.microsoft.com/identity/claims/openid2_id</span></span>|
|<span data-ttu-id="69091-269">http://schemas.microsoft.com/identity/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="69091-269">http://schemas.microsoft.com/identity/claims/identityprovider</span></span>|
|<span data-ttu-id="69091-270">http://schemas.microsoft.com/identity/claims/objectidentifier</span><span class="sxs-lookup"><span data-stu-id="69091-270">http://schemas.microsoft.com/identity/claims/objectidentifier</span></span>|
|<span data-ttu-id="69091-271">http://schemas.microsoft.com/identity/claims/puid</span><span class="sxs-lookup"><span data-stu-id="69091-271">http://schemas.microsoft.com/identity/claims/puid</span></span>|
|<span data-ttu-id="69091-272">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span><span class="sxs-lookup"><span data-stu-id="69091-272">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span></span> |
|<span data-ttu-id="69091-273">http://schemas.microsoft.com/identity/claims/tenantid</span><span class="sxs-lookup"><span data-stu-id="69091-273">http://schemas.microsoft.com/identity/claims/tenantid</span></span>|
|<span data-ttu-id="69091-274">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="69091-274">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span>|
|<span data-ttu-id="69091-275">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="69091-275">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span>|
|<span data-ttu-id="69091-276">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="69091-276">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span></span>|
|<span data-ttu-id="69091-277">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span><span class="sxs-lookup"><span data-stu-id="69091-277">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span></span>|
|<span data-ttu-id="69091-278">http://schemas.microsoft.com/claims/groups.link</span><span class="sxs-lookup"><span data-stu-id="69091-278">http://schemas.microsoft.com/claims/groups.link</span></span>|
|<span data-ttu-id="69091-279">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span><span class="sxs-lookup"><span data-stu-id="69091-279">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span></span>|
|<span data-ttu-id="69091-280">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span><span class="sxs-lookup"><span data-stu-id="69091-280">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span></span>|
|<span data-ttu-id="69091-281">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span><span class="sxs-lookup"><span data-stu-id="69091-281">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span></span>|
|<span data-ttu-id="69091-282">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span><span class="sxs-lookup"><span data-stu-id="69091-282">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span></span>|
|<span data-ttu-id="69091-283">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span><span class="sxs-lookup"><span data-stu-id="69091-283">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span></span>|
|<span data-ttu-id="69091-284">http://schemas.microsoft.com/2014/03/psso</span><span class="sxs-lookup"><span data-stu-id="69091-284">http://schemas.microsoft.com/2014/03/psso</span></span>|
|<span data-ttu-id="69091-285">http://schemas.microsoft.com/claims/authnmethodsreferences</span><span class="sxs-lookup"><span data-stu-id="69091-285">http://schemas.microsoft.com/claims/authnmethodsreferences</span></span>|
|<span data-ttu-id="69091-286">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span><span class="sxs-lookup"><span data-stu-id="69091-286">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span></span>|
|<span data-ttu-id="69091-287">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span><span class="sxs-lookup"><span data-stu-id="69091-287">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span></span>|
|<span data-ttu-id="69091-288">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span><span class="sxs-lookup"><span data-stu-id="69091-288">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span></span>|
|<span data-ttu-id="69091-289">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span><span class="sxs-lookup"><span data-stu-id="69091-289">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span></span>|
|<span data-ttu-id="69091-290">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span><span class="sxs-lookup"><span data-stu-id="69091-290">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span></span>|
|<span data-ttu-id="69091-291">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span><span class="sxs-lookup"><span data-stu-id="69091-291">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span></span>|
|<span data-ttu-id="69091-292">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span><span class="sxs-lookup"><span data-stu-id="69091-292">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span></span>|
|<span data-ttu-id="69091-293">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span><span class="sxs-lookup"><span data-stu-id="69091-293">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span></span>|
|<span data-ttu-id="69091-294">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span><span class="sxs-lookup"><span data-stu-id="69091-294">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span></span>|
|<span data-ttu-id="69091-295">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span><span class="sxs-lookup"><span data-stu-id="69091-295">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span></span>|
|<span data-ttu-id="69091-296">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span><span class="sxs-lookup"><span data-stu-id="69091-296">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span></span>|
|<span data-ttu-id="69091-297">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span><span class="sxs-lookup"><span data-stu-id="69091-297">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span></span>|
|<span data-ttu-id="69091-298">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="69091-298">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span></span>|
|<span data-ttu-id="69091-299">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span><span class="sxs-lookup"><span data-stu-id="69091-299">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span></span>|
|<span data-ttu-id="69091-300">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="69091-300">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span></span>|
|<span data-ttu-id="69091-301">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span><span class="sxs-lookup"><span data-stu-id="69091-301">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span></span>|
|<span data-ttu-id="69091-302">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span><span class="sxs-lookup"><span data-stu-id="69091-302">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span></span>|
|<span data-ttu-id="69091-303">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span><span class="sxs-lookup"><span data-stu-id="69091-303">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span></span>|
|<span data-ttu-id="69091-304">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span><span class="sxs-lookup"><span data-stu-id="69091-304">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span></span>|
|<span data-ttu-id="69091-305">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span><span class="sxs-lookup"><span data-stu-id="69091-305">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span></span>|
|<span data-ttu-id="69091-306">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span><span class="sxs-lookup"><span data-stu-id="69091-306">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span></span>|
|<span data-ttu-id="69091-307">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span><span class="sxs-lookup"><span data-stu-id="69091-307">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span></span>|
|<span data-ttu-id="69091-308">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span><span class="sxs-lookup"><span data-stu-id="69091-308">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span></span>|
|<span data-ttu-id="69091-309">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span><span class="sxs-lookup"><span data-stu-id="69091-309">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span></span>|
|<span data-ttu-id="69091-310">http://schemas.microsoft.com/identity/claims/scope</span><span class="sxs-lookup"><span data-stu-id="69091-310">http://schemas.microsoft.com/identity/claims/scope</span></span>|

## <a name="claims-mapping-policy-properties"></a><span data-ttu-id="69091-311">클레임 매핑 정책 속성</span><span class="sxs-lookup"><span data-stu-id="69091-311">Claims mapping policy properties</span></span>
<span data-ttu-id="69091-312">클레임을 내보낸 정책 toocontrol 매핑 클레임의 hello 속성을 사용 하 고 hello 데이터에서 소싱 된 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-312">Use hello properties of a claims mapping policy toocontrol which claims are emitted, and where hello data is sourced from.</span></span> <span data-ttu-id="69091-313">설정 된 정책이 hello 시스템 hello 코어 클레임 집합을 포함 하는 토큰을 발급, hello 기본 클레임 집합을 및 응용 프로그램 hello 하는 선택적 클레임 tooreceive 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-313">If no policy is set, hello system issues tokens containing hello core claim set, hello basic claim set, and any optional claims that hello application has chosen tooreceive.</span></span>

### <a name="include-basic-claim-set"></a><span data-ttu-id="69091-314">기본 클레임 집합 포함</span><span class="sxs-lookup"><span data-stu-id="69091-314">Include basic claim set</span></span>

<span data-ttu-id="69091-315">**문자열:** IncludeBasicClaimSet</span><span class="sxs-lookup"><span data-stu-id="69091-315">**String:** IncludeBasicClaimSet</span></span>

<span data-ttu-id="69091-316">**데이터 형식:** 부울(True 또는 False)</span><span class="sxs-lookup"><span data-stu-id="69091-316">**Data type:** Boolean (True or False)</span></span>

<span data-ttu-id="69091-317">**요약:** 이 속성은이 정책에 의해 영향을 받는 토큰에 hello 기본 클레임 집합에 포함 되는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-317">**Summary:** This property determines whether hello basic claim set is included in tokens affected by this policy.</span></span> 

- <span data-ttu-id="69091-318">경우 hello 정책에 의해 영향을 받은 토큰의 집합 tooTrue, hello 기본 클레임 집합의 모든 클레임을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="69091-318">If set tooTrue, all claims in hello basic claim set are emitted in tokens affected by hello policy.</span></span> 
- <span data-ttu-id="69091-319">집합 tooFalse, hello 기본 클레임 집합의 클레임에에서 없는 경우 hello 토큰은 개별적으로 추가 hello의 hello 클레임 스키마 속성에 동일한 정책.</span><span class="sxs-lookup"><span data-stu-id="69091-319">If set tooFalse, claims in hello basic claim set are not in hello tokens, unless they are individually added in hello claims schema property of hello same policy.</span></span>

>[!NOTE] 
><span data-ttu-id="69091-320">Hello 코어의 클레임 집합은이 속성은로 설정 하는 것에 관계 없이 모든 토큰에 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-320">Claims in hello core claim set are present in every token, regardless of what this property is set to.</span></span> 

### <a name="claims-schema"></a><span data-ttu-id="69091-321">클레임 스키마</span><span class="sxs-lookup"><span data-stu-id="69091-321">Claims schema</span></span>

<span data-ttu-id="69091-322">**문자열:** ClaimsSchema</span><span class="sxs-lookup"><span data-stu-id="69091-322">**String:** ClaimsSchema</span></span>

<span data-ttu-id="69091-323">**데이터 형식:** 하나 이상의 클레임 스키마 항목을 가진 JSON Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-323">**Data type:** JSON blob with one or more claim schema entries</span></span>

<span data-ttu-id="69091-324">**요약:** 이 속성은 hello 정책에 의해 영향을 받는 hello 토큰에 표시 되는 클레임을 정의 또한 toohello 기본 클레임 집합 및 hello 코어 클레임 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-324">**Summary:** This property defines which claims are present in hello tokens affected by hello policy, in addition toohello basic claim set and hello core claim set.</span></span>
<span data-ttu-id="69091-325">이 속성에 정의된 각 클레임 스키마 항목의 경우 특정 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-325">For each claim schema entry defined in this property, certain information is required.</span></span> <span data-ttu-id="69091-326">Hello 데이터에서 온 것인지를 지정 해야 합니다 (**값** 또는 **소스/i D 쌍**)로 내보내는 hello 데이터 클레임 및 (**클레임 유형**).</span><span class="sxs-lookup"><span data-stu-id="69091-326">You must specify where hello data is coming from (**Value** or **Source/ID pair**), and which claim hello data is emitted as (**Claim Type**).</span></span>

### <a name="claim-schema-entry-elements"></a><span data-ttu-id="69091-327">클레임 스키마 항목 요소</span><span class="sxs-lookup"><span data-stu-id="69091-327">Claim schema entry elements</span></span>

<span data-ttu-id="69091-328">**값:** hello Value 요소 hello 클레임에 포함 된 hello 데이터 toobe로 정적 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-328">**Value:** hello Value element defines a static value as hello data toobe emitted in hello claim.</span></span>

<span data-ttu-id="69091-329">**소스/i D 쌍:** 소스 hello 및에서 hello hello 클레임에는 데이터 원본으로 ID 요소를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-329">**Source/ID pair:** hello Source and ID elements define where hello data in hello claim is sourced from.</span></span> 

<span data-ttu-id="69091-330">hello 소스 요소는 hello 다음의 tooone를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-330">hello Source element must be set tooone of hello following:</span></span> 


- <span data-ttu-id="69091-331">"user": hello 데이터 hello에 클레임은 hello 사용자 개체에 대 한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-331">"user": hello data in hello claim is a property on hello User object.</span></span> 
- <span data-ttu-id="69091-332">"application": hello 데이터 hello에 클레임은 hello (클라이언트) 응용 프로그램 서비스 사용자에 대 한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-332">"application": hello data in hello claim is a property on hello application (client) service principal.</span></span> 
- <span data-ttu-id="69091-333">"resource": hello 데이터 hello에 클레임은 hello 리소스 서비스 사용자에 대 한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-333">"resource": hello data in hello claim is a property on hello resource service principal.</span></span>
- <span data-ttu-id="69091-334">"audience": hello 클레임의 hello 데이터는 대상인 hello hello 토큰 (두 hello 클라이언트 또는 리소스 서비스 사용자)의 hello 서비스 사용자에 대 한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-334">"audience": hello data in hello claim is a property on hello service principal that is hello audience of hello token (either hello client or resource service principal).</span></span>
- <span data-ttu-id="69091-335">"company": hello 데이터 hello에 클레임은 hello 리소스 테 넌 트의 회사 개체에 대 한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-335">“company”: hello data in hello claim is a property on hello resource tenant’s Company object.</span></span>
- <span data-ttu-id="69091-336">"변환": hello 데이터 hello에 클레임은 클레임 변환에서 (이 문서의 뒷부분에 나오는 "클레임 변환" hello 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="69091-336">"transformation": hello data in hello claim is from claims transformation (see hello "Claims transformation" section later in this article).</span></span> 

<span data-ttu-id="69091-337">Hello 원본이 변환 인 경우 hello **TransformationID** 요소는이 클레임 정의에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-337">If hello source is transformation, hello **TransformationID** element must be included in this claim definition as well.</span></span>

<span data-ttu-id="69091-338">hello ID 요소 hello 클레임에 대 한 hello 값을 제공 하는 hello 소스에서 되는 속성을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-338">hello ID element identifies which property on hello source provides hello value for hello claim.</span></span> <span data-ttu-id="69091-339">hello 다음 표에서 hello 값 id 원본의 각 값에 대해 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-339">hello following table lists hello values of ID valid for each value of Source.</span></span>

#### <a name="table-3-valid-id-values-per-source"></a><span data-ttu-id="69091-340">표 3: 원본별 유효한 ID 값</span><span class="sxs-lookup"><span data-stu-id="69091-340">Table 3: Valid ID values per source</span></span>
|<span data-ttu-id="69091-341">원본</span><span class="sxs-lookup"><span data-stu-id="69091-341">Source</span></span>|<span data-ttu-id="69091-342">ID</span><span class="sxs-lookup"><span data-stu-id="69091-342">ID</span></span>|<span data-ttu-id="69091-343">설명</span><span class="sxs-lookup"><span data-stu-id="69091-343">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="69091-344">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-344">User</span></span>|<span data-ttu-id="69091-345">surname</span><span class="sxs-lookup"><span data-stu-id="69091-345">surname</span></span>|<span data-ttu-id="69091-346">성</span><span class="sxs-lookup"><span data-stu-id="69091-346">Family Name</span></span>|
|<span data-ttu-id="69091-347">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-347">User</span></span>|<span data-ttu-id="69091-348">givenname</span><span class="sxs-lookup"><span data-stu-id="69091-348">givenname</span></span>|<span data-ttu-id="69091-349">이름</span><span class="sxs-lookup"><span data-stu-id="69091-349">Given Name</span></span>|
|<span data-ttu-id="69091-350">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-350">User</span></span>|<span data-ttu-id="69091-351">displayname</span><span class="sxs-lookup"><span data-stu-id="69091-351">displayname</span></span>|<span data-ttu-id="69091-352">표시 이름</span><span class="sxs-lookup"><span data-stu-id="69091-352">Display Name</span></span>|
|<span data-ttu-id="69091-353">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-353">User</span></span>|<span data-ttu-id="69091-354">objectId</span><span class="sxs-lookup"><span data-stu-id="69091-354">objectid</span></span>|<span data-ttu-id="69091-355">ObjectID</span><span class="sxs-lookup"><span data-stu-id="69091-355">ObjectID</span></span>|
|<span data-ttu-id="69091-356">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-356">User</span></span>|<span data-ttu-id="69091-357">mail</span><span class="sxs-lookup"><span data-stu-id="69091-357">mail</span></span>|<span data-ttu-id="69091-358">메일 주소</span><span class="sxs-lookup"><span data-stu-id="69091-358">Email Address</span></span>|
|<span data-ttu-id="69091-359">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-359">User</span></span>|<span data-ttu-id="69091-360">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="69091-360">userprincipalname</span></span>|<span data-ttu-id="69091-361">사용자 계정 이름</span><span class="sxs-lookup"><span data-stu-id="69091-361">User Principal Name</span></span>|
|<span data-ttu-id="69091-362">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-362">User</span></span>|<span data-ttu-id="69091-363">department</span><span class="sxs-lookup"><span data-stu-id="69091-363">department</span></span>|<span data-ttu-id="69091-364">department</span><span class="sxs-lookup"><span data-stu-id="69091-364">Department</span></span>|
|<span data-ttu-id="69091-365">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-365">User</span></span>|<span data-ttu-id="69091-366">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="69091-366">onpremisessamaccountname</span></span>|<span data-ttu-id="69091-367">온-프레미스 SAM 계정 이름</span><span class="sxs-lookup"><span data-stu-id="69091-367">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="69091-368">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-368">User</span></span>|<span data-ttu-id="69091-369">netbiosname</span><span class="sxs-lookup"><span data-stu-id="69091-369">netbiosname</span></span>|<span data-ttu-id="69091-370">NetBios 이름</span><span class="sxs-lookup"><span data-stu-id="69091-370">NetBios Name</span></span>|
|<span data-ttu-id="69091-371">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-371">User</span></span>|<span data-ttu-id="69091-372">dnsdomainname</span><span class="sxs-lookup"><span data-stu-id="69091-372">dnsdomainname</span></span>|<span data-ttu-id="69091-373">DNS 도메인 이름</span><span class="sxs-lookup"><span data-stu-id="69091-373">Dns Domain Name</span></span>|
|<span data-ttu-id="69091-374">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-374">User</span></span>|<span data-ttu-id="69091-375">onpremisesecurityidentifier</span><span class="sxs-lookup"><span data-stu-id="69091-375">onpremisesecurityidentifier</span></span>|<span data-ttu-id="69091-376">온-프레미스 보안 식별자</span><span class="sxs-lookup"><span data-stu-id="69091-376">on-premises Security Identifier</span></span>|
|<span data-ttu-id="69091-377">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-377">User</span></span>|<span data-ttu-id="69091-378">companyname</span><span class="sxs-lookup"><span data-stu-id="69091-378">companyname</span></span>|<span data-ttu-id="69091-379">조직 이름</span><span class="sxs-lookup"><span data-stu-id="69091-379">Organization Name</span></span>|
|<span data-ttu-id="69091-380">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-380">User</span></span>|<span data-ttu-id="69091-381">streetaddress</span><span class="sxs-lookup"><span data-stu-id="69091-381">streetaddress</span></span>|<span data-ttu-id="69091-382">주소</span><span class="sxs-lookup"><span data-stu-id="69091-382">Street Address</span></span>|
|<span data-ttu-id="69091-383">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-383">User</span></span>|<span data-ttu-id="69091-384">postalcode</span><span class="sxs-lookup"><span data-stu-id="69091-384">postalcode</span></span>|<span data-ttu-id="69091-385">우편 번호</span><span class="sxs-lookup"><span data-stu-id="69091-385">Postal Code</span></span>|
|<span data-ttu-id="69091-386">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-386">User</span></span>|<span data-ttu-id="69091-387">preferredlanguange</span><span class="sxs-lookup"><span data-stu-id="69091-387">preferredlanguange</span></span>|<span data-ttu-id="69091-388">기본 설정 언어</span><span class="sxs-lookup"><span data-stu-id="69091-388">Preferred Language</span></span>|
|<span data-ttu-id="69091-389">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-389">User</span></span>|<span data-ttu-id="69091-390">onpremisesuserprincipalname</span><span class="sxs-lookup"><span data-stu-id="69091-390">onpremisesuserprincipalname</span></span>|<span data-ttu-id="69091-391">온-프레미스 UPN</span><span class="sxs-lookup"><span data-stu-id="69091-391">on-premises UPN</span></span>|
|<span data-ttu-id="69091-392">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-392">User</span></span>|<span data-ttu-id="69091-393">mailNickname</span><span class="sxs-lookup"><span data-stu-id="69091-393">mailnickname</span></span>|<span data-ttu-id="69091-394">메일 애칭</span><span class="sxs-lookup"><span data-stu-id="69091-394">Mail Nickname</span></span>|
|<span data-ttu-id="69091-395">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-395">User</span></span>|<span data-ttu-id="69091-396">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="69091-396">extensionattribute1</span></span>|<span data-ttu-id="69091-397">확장 특성 1</span><span class="sxs-lookup"><span data-stu-id="69091-397">Extension Attribute 1</span></span>|
|<span data-ttu-id="69091-398">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-398">User</span></span>|<span data-ttu-id="69091-399">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="69091-399">extensionattribute2</span></span>|<span data-ttu-id="69091-400">확장 특성 2</span><span class="sxs-lookup"><span data-stu-id="69091-400">Extension Attribute 2</span></span>|
|<span data-ttu-id="69091-401">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-401">User</span></span>|<span data-ttu-id="69091-402">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="69091-402">extensionattribute3</span></span>|<span data-ttu-id="69091-403">확장 특성 3</span><span class="sxs-lookup"><span data-stu-id="69091-403">Extension Attribute 3</span></span>|
|<span data-ttu-id="69091-404">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-404">User</span></span>|<span data-ttu-id="69091-405">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="69091-405">extensionattribute4</span></span>|<span data-ttu-id="69091-406">확장 특성 4</span><span class="sxs-lookup"><span data-stu-id="69091-406">Extension Attribute 4</span></span>|
|<span data-ttu-id="69091-407">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-407">User</span></span>|<span data-ttu-id="69091-408">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="69091-408">extensionattribute5</span></span>|<span data-ttu-id="69091-409">확장 특성 5</span><span class="sxs-lookup"><span data-stu-id="69091-409">Extension Attribute 5</span></span>|
|<span data-ttu-id="69091-410">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-410">User</span></span>|<span data-ttu-id="69091-411">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="69091-411">extensionattribute6</span></span>|<span data-ttu-id="69091-412">확장 특성 6</span><span class="sxs-lookup"><span data-stu-id="69091-412">Extension Attribute 6</span></span>|
|<span data-ttu-id="69091-413">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-413">User</span></span>|<span data-ttu-id="69091-414">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="69091-414">extensionattribute7</span></span>|<span data-ttu-id="69091-415">확장 특성 7</span><span class="sxs-lookup"><span data-stu-id="69091-415">Extension Attribute 7</span></span>|
|<span data-ttu-id="69091-416">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-416">User</span></span>|<span data-ttu-id="69091-417">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="69091-417">extensionattribute8</span></span>|<span data-ttu-id="69091-418">확장 특성 8</span><span class="sxs-lookup"><span data-stu-id="69091-418">Extension Attribute 8</span></span>|
|<span data-ttu-id="69091-419">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-419">User</span></span>|<span data-ttu-id="69091-420">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="69091-420">extensionattribute9</span></span>|<span data-ttu-id="69091-421">확장 특성 9</span><span class="sxs-lookup"><span data-stu-id="69091-421">Extension Attribute 9</span></span>|
|<span data-ttu-id="69091-422">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-422">User</span></span>|<span data-ttu-id="69091-423">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="69091-423">extensionattribute10</span></span>|<span data-ttu-id="69091-424">확장 특성 10</span><span class="sxs-lookup"><span data-stu-id="69091-424">Extension Attribute 10</span></span>|
|<span data-ttu-id="69091-425">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-425">User</span></span>|<span data-ttu-id="69091-426">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="69091-426">extensionattribute11</span></span>|<span data-ttu-id="69091-427">확장 특성 11</span><span class="sxs-lookup"><span data-stu-id="69091-427">Extension Attribute 11</span></span>|
|<span data-ttu-id="69091-428">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-428">User</span></span>|<span data-ttu-id="69091-429">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="69091-429">extensionattribute12</span></span>|<span data-ttu-id="69091-430">확장 특성 12</span><span class="sxs-lookup"><span data-stu-id="69091-430">Extension Attribute 12</span></span>|
|<span data-ttu-id="69091-431">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-431">User</span></span>|<span data-ttu-id="69091-432">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="69091-432">extensionattribute13</span></span>|<span data-ttu-id="69091-433">확장 특성 13</span><span class="sxs-lookup"><span data-stu-id="69091-433">Extension Attribute 13</span></span>|
|<span data-ttu-id="69091-434">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-434">User</span></span>|<span data-ttu-id="69091-435">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="69091-435">extensionattribute14</span></span>|<span data-ttu-id="69091-436">확장 특성 14</span><span class="sxs-lookup"><span data-stu-id="69091-436">Extension Attribute 14</span></span>|
|<span data-ttu-id="69091-437">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-437">User</span></span>|<span data-ttu-id="69091-438">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="69091-438">extensionattribute15</span></span>|<span data-ttu-id="69091-439">확장 특성 15</span><span class="sxs-lookup"><span data-stu-id="69091-439">Extension Attribute 15</span></span>|
|<span data-ttu-id="69091-440">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-440">User</span></span>|<span data-ttu-id="69091-441">othermail</span><span class="sxs-lookup"><span data-stu-id="69091-441">othermail</span></span>|<span data-ttu-id="69091-442">다른 메일</span><span class="sxs-lookup"><span data-stu-id="69091-442">Other Mail</span></span>|
|<span data-ttu-id="69091-443">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-443">User</span></span>|<span data-ttu-id="69091-444">country</span><span class="sxs-lookup"><span data-stu-id="69091-444">country</span></span>|<span data-ttu-id="69091-445">국가</span><span class="sxs-lookup"><span data-stu-id="69091-445">Country</span></span>|
|<span data-ttu-id="69091-446">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-446">User</span></span>|<span data-ttu-id="69091-447">city</span><span class="sxs-lookup"><span data-stu-id="69091-447">city</span></span>|<span data-ttu-id="69091-448">City</span><span class="sxs-lookup"><span data-stu-id="69091-448">City</span></span>|
|<span data-ttu-id="69091-449">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-449">User</span></span>|<span data-ttu-id="69091-450">state</span><span class="sxs-lookup"><span data-stu-id="69091-450">state</span></span>|<span data-ttu-id="69091-451">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="69091-451">State</span></span>|
|<span data-ttu-id="69091-452">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-452">User</span></span>|<span data-ttu-id="69091-453">jobtitle</span><span class="sxs-lookup"><span data-stu-id="69091-453">jobtitle</span></span>|<span data-ttu-id="69091-454">직위</span><span class="sxs-lookup"><span data-stu-id="69091-454">Job Title</span></span>|
|<span data-ttu-id="69091-455">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-455">User</span></span>|<span data-ttu-id="69091-456">employeeid</span><span class="sxs-lookup"><span data-stu-id="69091-456">employeeid</span></span>|<span data-ttu-id="69091-457">직원 ID</span><span class="sxs-lookup"><span data-stu-id="69091-457">Employee ID</span></span>|
|<span data-ttu-id="69091-458">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-458">User</span></span>|<span data-ttu-id="69091-459">facsimiletelephonenumber</span><span class="sxs-lookup"><span data-stu-id="69091-459">facsimiletelephonenumber</span></span>|<span data-ttu-id="69091-460">팩스 번호</span><span class="sxs-lookup"><span data-stu-id="69091-460">Facsimile Telephone Number</span></span>|
|<span data-ttu-id="69091-461">응용 프로그램, 리소스, 대상 그룹</span><span class="sxs-lookup"><span data-stu-id="69091-461">application, resource, audience</span></span>|<span data-ttu-id="69091-462">displayname</span><span class="sxs-lookup"><span data-stu-id="69091-462">displayname</span></span>|<span data-ttu-id="69091-463">표시 이름</span><span class="sxs-lookup"><span data-stu-id="69091-463">Display Name</span></span>|
|<span data-ttu-id="69091-464">응용 프로그램, 리소스, 대상 그룹</span><span class="sxs-lookup"><span data-stu-id="69091-464">application, resource, audience</span></span>|<span data-ttu-id="69091-465">objected</span><span class="sxs-lookup"><span data-stu-id="69091-465">objected</span></span>|<span data-ttu-id="69091-466">ObjectID</span><span class="sxs-lookup"><span data-stu-id="69091-466">ObjectID</span></span>|
|<span data-ttu-id="69091-467">응용 프로그램, 리소스, 대상 그룹</span><span class="sxs-lookup"><span data-stu-id="69091-467">application, resource, audience</span></span>|<span data-ttu-id="69091-468">tags</span><span class="sxs-lookup"><span data-stu-id="69091-468">tags</span></span>|<span data-ttu-id="69091-469">서비스 주체 태그</span><span class="sxs-lookup"><span data-stu-id="69091-469">Service Principal Tag</span></span>|
|<span data-ttu-id="69091-470">회사</span><span class="sxs-lookup"><span data-stu-id="69091-470">Company</span></span>|<span data-ttu-id="69091-471">tenantcountry</span><span class="sxs-lookup"><span data-stu-id="69091-471">tenantcountry</span></span>|<span data-ttu-id="69091-472">테넌트 국가</span><span class="sxs-lookup"><span data-stu-id="69091-472">Tenant’s country</span></span>|

<span data-ttu-id="69091-473">**TransformationID:** hello TransformationID 요소는 소스 요소가 너무 설정 되는 경우에 hello 제공 해야 합니다. "변환"입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-473">**TransformationID:** hello TransformationID element must be provided only if hello Source element is set too“transformation”.</span></span>

- <span data-ttu-id="69091-474">이 요소에는 hello에 hello 변형 항목의 ID 요소 hello와 일치 해야 **ClaimsTransformation** 이 클레임에 대 한 hello 데이터 생성 되는 방식을 정의 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-474">This element must match hello ID element of hello transformation entry in hello **ClaimsTransformation** property that defines how hello data for this claim is generated.</span></span>

<span data-ttu-id="69091-475">**클레임 유형:** hello **JwtClaimType** 및 **SamlClaimType** 요소 클레임 스키마 항목이이 참조 하는 클레임을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-475">**Claim Type:** hello **JwtClaimType** and **SamlClaimType** elements define which claim this claim schema entry refers to.</span></span>

- <span data-ttu-id="69091-476">hello JwtClaimType hello hello 클레임 toobe Jwt에 포함 된 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-476">hello JwtClaimType must contain hello name of hello claim toobe emitted in JWTs.</span></span>
- <span data-ttu-id="69091-477">hello SamlClaimType hello hello의 URI toobe SAML 토큰에 포함 된 클레임을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-477">hello SamlClaimType must contain hello URI of hello claim toobe emitted in SAML tokens.</span></span>

>[!NOTE]
><span data-ttu-id="69091-478">이름 및 Uri hello에 있는 클레임의 제한 클레임 집합 hello 클레임 형식 요소에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-478">Names and URIs of claims in hello restricted claim set cannot be used for hello claim type elements.</span></span> <span data-ttu-id="69091-479">자세한 내용은이 문서의 뒷부분에 나오는 hello "예외 및 제한 사항" 섹션을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-479">For more information, see hello "Exceptions and restrictions" section later in this article.</span></span>

### <a name="claims-transformation"></a><span data-ttu-id="69091-480">클레임 변환</span><span class="sxs-lookup"><span data-stu-id="69091-480">Claims transformation</span></span>

<span data-ttu-id="69091-481">**문자열:** ClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="69091-481">**String:** ClaimsTransformation</span></span>

<span data-ttu-id="69091-482">**데이터 형식:** 하나 이상의 변환 항목을 가진 JSON Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-482">**Data type:** JSON blob, with one or more transformation entries</span></span> 

<span data-ttu-id="69091-483">**요약:** toogenerate hello 출력 데이터에 지정 된 클레임에 대 한 hello 클레임 스키마를이 속성 tooapply 일반적인 변환 toosource 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-483">**Summary:** Use this property tooapply common transformations toosource data, toogenerate hello output data for claims specified in hello Claims Schema.</span></span>

<span data-ttu-id="69091-484">**ID:** 사용 하 여 hello ID 요소 tooreference hello TransformationID 클레임 스키마 항목에서에서이 변환 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-484">**ID:** Use hello ID element tooreference this transformation entry in hello TransformationID Claims Schema entry.</span></span> <span data-ttu-id="69091-485">이 값은 이 정책 내에서 각 변환 항목에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-485">This value must be unique for each transformation entry within this policy.</span></span>

<span data-ttu-id="69091-486">**TransformationMethod:** hello TransformationMethod 요소는 작업은 수행된 toogenerate hello 데이터 hello 클레임에 대 한 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-486">**TransformationMethod:** hello TransformationMethod element identifies which operation is performed toogenerate hello data for hello claim.</span></span>

<span data-ttu-id="69091-487">선택한 hello 방법에 따라, 입력 및 출력의 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-487">Based on hello method chosen, a set of inputs and outputs is expected.</span></span> <span data-ttu-id="69091-488">Hello를 사용 하 여 정의 되며 **InputClaims**, **InputParameters** 및 **OutputClaims** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-488">These are defined by using hello **InputClaims**, **InputParameters** and **OutputClaims** elements.</span></span>

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a><span data-ttu-id="69091-489">표 4: 변환 메서드 및 예상 입력 및 출력</span><span class="sxs-lookup"><span data-stu-id="69091-489">Table 4: Transformation methods and expected inputs and outputs</span></span>
|<span data-ttu-id="69091-490">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="69091-490">TransformationMethod</span></span>|<span data-ttu-id="69091-491">예상 입력</span><span class="sxs-lookup"><span data-stu-id="69091-491">Expected input</span></span>|<span data-ttu-id="69091-492">예상 출력</span><span class="sxs-lookup"><span data-stu-id="69091-492">Expected output</span></span>|<span data-ttu-id="69091-493">설명</span><span class="sxs-lookup"><span data-stu-id="69091-493">Description</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="69091-494">Join</span><span class="sxs-lookup"><span data-stu-id="69091-494">Join</span></span>|<span data-ttu-id="69091-495">string1, string2, 구분 기호</span><span class="sxs-lookup"><span data-stu-id="69091-495">string1, string2, separator</span></span>|<span data-ttu-id="69091-496">outputClaim</span><span class="sxs-lookup"><span data-stu-id="69091-496">outputClaim</span></span>|<span data-ttu-id="69091-497">구분 기호를 사용하여 입력 문자열을 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-497">Joins input strings by using a separator in between.</span></span> <span data-ttu-id="69091-498">예: string1:"foo@bar.com" , string2:"sandbox" , separator:"."는 outputClaim:"foo@bar.com.sandbox"를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-498">For example: string1:"foo@bar.com" , string2:"sandbox" , separator:"." results in outputClaim:"foo@bar.com.sandbox"</span></span>|
|<span data-ttu-id="69091-499">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="69091-499">ExtractMailPrefix</span></span>|<span data-ttu-id="69091-500">mail</span><span class="sxs-lookup"><span data-stu-id="69091-500">mail</span></span>|<span data-ttu-id="69091-501">outputClaim</span><span class="sxs-lookup"><span data-stu-id="69091-501">outputClaim</span></span>|<span data-ttu-id="69091-502">Hello 전자 메일 주소의 로컬 부분을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-502">Extracts hello local part of an email address.</span></span> <span data-ttu-id="69091-503">예: mail:"foo@bar.com"은 outputClaim:"foo"를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-503">For example: mail:"foo@bar.com" results in outputClaim:"foo".</span></span> <span data-ttu-id="69091-504">@ 하지 않는 경우 부호가 있는, hello 원래 입력된 문자열은 있는 그대로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69091-504">If no @ sign is present, then hello orignal input string is returned as is.</span></span>|

<span data-ttu-id="69091-505">**InputClaims:** 는 InputClaims 요소 toopass hello 데이터 클레임 스키마 항목 tooa 변환을를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-505">**InputClaims:** Use an InputClaims element toopass hello data from a claim schema entry tooa transformation.</span></span> <span data-ttu-id="69091-506">두 개의 특성인 **ClaimTypeReferenceId** 및 **TransformationClaimType**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-506">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="69091-507">**ClaimTypeReferenceId** hello 클레임 스키마 항목 toofind hello 적절 한 입력된 클레임의 ID 요소와 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-507">**ClaimTypeReferenceId** is joined with ID element of hello claim schema entry toofind hello appropriate input claim.</span></span> 
- <span data-ttu-id="69091-508">**TransformationClaimType** 가 사용 되는 toogive 고유 이름을 toothis 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-508">**TransformationClaimType** is used toogive a unique name toothis input.</span></span> <span data-ttu-id="69091-509">이 이름은 hello 변환 방법에 대 한 예상 hello 입력 중 하 나와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-509">This name must match one of hello expected inputs for hello transformation method.</span></span>

<span data-ttu-id="69091-510">**InputParameters:** InputParameters 요소 toopass 상수 값 tooa 변환을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-510">**InputParameters:** Use an InputParameters element toopass a constant value tooa transformation.</span></span> <span data-ttu-id="69091-511">두 개의 특성인 **Value** 및 **ID**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-511">It has two attributes: **Value** and **ID**.</span></span>

- <span data-ttu-id="69091-512">**값** hello 상수 값을 실제 toobe 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69091-512">**Value** is hello actual constant value toobe passed.</span></span>
- <span data-ttu-id="69091-513">**ID** 가 사용 되는 toogive 고유 이름을 toothis 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-513">**ID** is used toogive a unique name toothis input.</span></span> <span data-ttu-id="69091-514">이 이름은 hello 변환 방법에 대 한 예상 hello 입력 중 하 나와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-514">This name must match one of hello expected inputs for hello transformation method.</span></span>

<span data-ttu-id="69091-515">**OutputClaims:** 변환에서 생성 되는 OutputClaims 요소 toohold hello 데이터를 사용 하 고 tooa 클레임 스키마 항목을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-515">**OutputClaims:** Use an OutputClaims element toohold hello data generated by a transformation, and tie it tooa claim schema entry.</span></span> <span data-ttu-id="69091-516">두 개의 특성인 **ClaimTypeReferenceId** 및 **TransformationClaimType**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-516">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="69091-517">**ClaimTypeReferenceId** hello hello 요청 스키마 항목 toofind hello 적절 한 출력 요청 ID와 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-517">**ClaimTypeReferenceId** is joined with hello ID of hello claim schema entry toofind hello appropriate output claim.</span></span>
- <span data-ttu-id="69091-518">**TransformationClaimType** 사용된 toogive는 고유한 이름을 toothis 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69091-518">**TransformationClaimType** is used toogive a unique name toothis output.</span></span> <span data-ttu-id="69091-519">이 이름은 hello 변환 방법에 대 한 예상 hello 출력 중 하나로 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-519">This name must match one of hello expected outputs for hello transformation method.</span></span>

### <a name="exceptions-and-restrictions"></a><span data-ttu-id="69091-520">예외 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="69091-520">Exceptions and restrictions</span></span>

<span data-ttu-id="69091-521">**SAML NameID 및 UPN:** hello NameID 및 UPN 값 소스와 hello 클레임 변환을 허용 되는 hello 특성은 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69091-521">**SAML NameID and UPN:** hello attributes from which you source hello NameID and UPN values, and hello claims transformations that are permitted, are limited.</span></span>

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a><span data-ttu-id="69091-522">표 5: SAML NameID에 대한 데이터 원본으로 허용되는 특성</span><span class="sxs-lookup"><span data-stu-id="69091-522">Table 5: Attributes allowed as a data source for SAML NameID</span></span>
|<span data-ttu-id="69091-523">원본</span><span class="sxs-lookup"><span data-stu-id="69091-523">Source</span></span>|<span data-ttu-id="69091-524">ID</span><span class="sxs-lookup"><span data-stu-id="69091-524">ID</span></span>|<span data-ttu-id="69091-525">설명</span><span class="sxs-lookup"><span data-stu-id="69091-525">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="69091-526">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-526">User</span></span>|<span data-ttu-id="69091-527">mail</span><span class="sxs-lookup"><span data-stu-id="69091-527">mail</span></span>|<span data-ttu-id="69091-528">메일 주소</span><span class="sxs-lookup"><span data-stu-id="69091-528">Email Address</span></span>|
|<span data-ttu-id="69091-529">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-529">User</span></span>|<span data-ttu-id="69091-530">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="69091-530">userprincipalname</span></span>|<span data-ttu-id="69091-531">사용자 계정 이름</span><span class="sxs-lookup"><span data-stu-id="69091-531">User Principal Name</span></span>|
|<span data-ttu-id="69091-532">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-532">User</span></span>|<span data-ttu-id="69091-533">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="69091-533">onpremisessamaccountname</span></span>|<span data-ttu-id="69091-534">온-프레미스 SAM 계정 이름</span><span class="sxs-lookup"><span data-stu-id="69091-534">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="69091-535">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-535">User</span></span>|<span data-ttu-id="69091-536">employeeid</span><span class="sxs-lookup"><span data-stu-id="69091-536">employeeid</span></span>|<span data-ttu-id="69091-537">직원 ID</span><span class="sxs-lookup"><span data-stu-id="69091-537">Employee ID</span></span>|
|<span data-ttu-id="69091-538">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-538">User</span></span>|<span data-ttu-id="69091-539">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="69091-539">extensionattribute1</span></span>|<span data-ttu-id="69091-540">확장 특성 1</span><span class="sxs-lookup"><span data-stu-id="69091-540">Extension Attribute 1</span></span>|
|<span data-ttu-id="69091-541">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-541">User</span></span>|<span data-ttu-id="69091-542">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="69091-542">extensionattribute2</span></span>|<span data-ttu-id="69091-543">확장 특성 2</span><span class="sxs-lookup"><span data-stu-id="69091-543">Extension Attribute 2</span></span>|
|<span data-ttu-id="69091-544">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-544">User</span></span>|<span data-ttu-id="69091-545">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="69091-545">extensionattribute3</span></span>|<span data-ttu-id="69091-546">확장 특성 3</span><span class="sxs-lookup"><span data-stu-id="69091-546">Extension Attribute 3</span></span>|
|<span data-ttu-id="69091-547">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-547">User</span></span>|<span data-ttu-id="69091-548">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="69091-548">extensionattribute4</span></span>|<span data-ttu-id="69091-549">확장 특성 4</span><span class="sxs-lookup"><span data-stu-id="69091-549">Extension Attribute 4</span></span>|
|<span data-ttu-id="69091-550">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-550">User</span></span>|<span data-ttu-id="69091-551">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="69091-551">extensionattribute5</span></span>|<span data-ttu-id="69091-552">확장 특성 5</span><span class="sxs-lookup"><span data-stu-id="69091-552">Extension Attribute 5</span></span>|
|<span data-ttu-id="69091-553">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-553">User</span></span>|<span data-ttu-id="69091-554">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="69091-554">extensionattribute6</span></span>|<span data-ttu-id="69091-555">확장 특성 6</span><span class="sxs-lookup"><span data-stu-id="69091-555">Extension Attribute 6</span></span>|
|<span data-ttu-id="69091-556">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-556">User</span></span>|<span data-ttu-id="69091-557">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="69091-557">extensionattribute7</span></span>|<span data-ttu-id="69091-558">확장 특성 7</span><span class="sxs-lookup"><span data-stu-id="69091-558">Extension Attribute 7</span></span>|
|<span data-ttu-id="69091-559">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-559">User</span></span>|<span data-ttu-id="69091-560">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="69091-560">extensionattribute8</span></span>|<span data-ttu-id="69091-561">확장 특성 8</span><span class="sxs-lookup"><span data-stu-id="69091-561">Extension Attribute 8</span></span>|
|<span data-ttu-id="69091-562">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-562">User</span></span>|<span data-ttu-id="69091-563">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="69091-563">extensionattribute9</span></span>|<span data-ttu-id="69091-564">확장 특성 9</span><span class="sxs-lookup"><span data-stu-id="69091-564">Extension Attribute 9</span></span>|
|<span data-ttu-id="69091-565">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-565">User</span></span>|<span data-ttu-id="69091-566">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="69091-566">extensionattribute10</span></span>|<span data-ttu-id="69091-567">확장 특성 10</span><span class="sxs-lookup"><span data-stu-id="69091-567">Extension Attribute 10</span></span>|
|<span data-ttu-id="69091-568">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-568">User</span></span>|<span data-ttu-id="69091-569">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="69091-569">extensionattribute11</span></span>|<span data-ttu-id="69091-570">확장 특성 11</span><span class="sxs-lookup"><span data-stu-id="69091-570">Extension Attribute 11</span></span>|
|<span data-ttu-id="69091-571">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-571">User</span></span>|<span data-ttu-id="69091-572">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="69091-572">extensionattribute12</span></span>|<span data-ttu-id="69091-573">확장 특성 12</span><span class="sxs-lookup"><span data-stu-id="69091-573">Extension Attribute 12</span></span>|
|<span data-ttu-id="69091-574">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-574">User</span></span>|<span data-ttu-id="69091-575">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="69091-575">extensionattribute13</span></span>|<span data-ttu-id="69091-576">확장 특성 13</span><span class="sxs-lookup"><span data-stu-id="69091-576">Extension Attribute 13</span></span>|
|<span data-ttu-id="69091-577">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-577">User</span></span>|<span data-ttu-id="69091-578">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="69091-578">extensionattribute14</span></span>|<span data-ttu-id="69091-579">확장 특성 14</span><span class="sxs-lookup"><span data-stu-id="69091-579">Extension Attribute 14</span></span>|
|<span data-ttu-id="69091-580">사용자</span><span class="sxs-lookup"><span data-stu-id="69091-580">User</span></span>|<span data-ttu-id="69091-581">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="69091-581">extensionattribute15</span></span>|<span data-ttu-id="69091-582">확장 특성 15</span><span class="sxs-lookup"><span data-stu-id="69091-582">Extension Attribute 15</span></span>|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a><span data-ttu-id="69091-583">표 6: SAML NameID에 허용되는 변환 메서드</span><span class="sxs-lookup"><span data-stu-id="69091-583">Table 6: Transformation methods allowed for SAML NameID</span></span>
|<span data-ttu-id="69091-584">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="69091-584">TransformationMethod</span></span>|<span data-ttu-id="69091-585">제한</span><span class="sxs-lookup"><span data-stu-id="69091-585">Restrictions</span></span>|
| ----- | ----- |
|<span data-ttu-id="69091-586">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="69091-586">ExtractMailPrefix</span></span>|<span data-ttu-id="69091-587">없음</span><span class="sxs-lookup"><span data-stu-id="69091-587">None</span></span>|
|<span data-ttu-id="69091-588">Join</span><span class="sxs-lookup"><span data-stu-id="69091-588">Join</span></span>|<span data-ttu-id="69091-589">조인 된 hello 접미사 hello 리소스 테 넌 트의 확인 된 도메인 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-589">hello suffix being joined must be a verified domain of hello resource tenant.</span></span>|

### <a name="custom-signing-key"></a><span data-ttu-id="69091-590">사용자 지정 서명 키</span><span class="sxs-lookup"><span data-stu-id="69091-590">Custom signing key</span></span>
<span data-ttu-id="69091-591">사용자 지정 서명 키 toohello 정책 tootake 효과 매핑 클레임에 대 한 서비스 사용자 개체를 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-591">A custom signing key must be assigned toohello service principal object for a claims mapping policy tootake effect.</span></span> <span data-ttu-id="69091-592">Hello 정책에 의해 영향을 받았는지는 발급 된 모든 토큰은이 키로 서명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69091-592">All tokens issued that have been impacted by hello policy are signed with this key.</span></span> <span data-ttu-id="69091-593">응용 프로그램에 구성 된 tooaccept 토큰이이 키로 서명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-593">Applications must be configured tooaccept tokens signed with this key.</span></span> <span data-ttu-id="69091-594">이렇게 하면 토큰의 hello hello 작성자에 의해 수정 된 승인 클레임 매핑 정책.</span><span class="sxs-lookup"><span data-stu-id="69091-594">This ensures acknowledgment that tokens have been modified by hello creator of hello claims mapping policy.</span></span> <span data-ttu-id="69091-595">이는 악의적인 행위자가 만든 클레임 매핑 정책으로부터 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-595">This protects applications from claims mapping policies created by malicious actors.</span></span>

### <a name="cross-tenant-scenarios"></a><span data-ttu-id="69091-596">교차 테넌트 시나리오</span><span class="sxs-lookup"><span data-stu-id="69091-596">Cross-tenant scenarios</span></span>
<span data-ttu-id="69091-597">클레임 정책 매핑 tooguest 사용자가 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-597">Claims mapping policies do not apply tooguest users.</span></span> <span data-ttu-id="69091-598">게스트 사용자가 tooaccess 응용 프로그램을 클레임 매핑 할당 된 정책 tooits 서비스 보안 주체, hello 기본 토큰이 발급 됩니다 (hello 정책은 어떤 영향도 주지).</span><span class="sxs-lookup"><span data-stu-id="69091-598">If a guest user attempts tooaccess an application with a claims mapping policy assigned tooits service principal, hello default token is issued (hello policy has no effect).</span></span>

## <a name="claims-mapping-policy-assignment"></a><span data-ttu-id="69091-599">클레임 매핑 정책 할당</span><span class="sxs-lookup"><span data-stu-id="69091-599">Claims mapping policy assignment</span></span>
<span data-ttu-id="69091-600">클레임 매핑 정책은 수만 할당 될 tooservice principal 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-600">Claims mapping policies can only be assigned tooservice principal objects.</span></span>

### <a name="example-claims-mapping-policies"></a><span data-ttu-id="69091-601">예제 클레임 매핑 정책</span><span class="sxs-lookup"><span data-stu-id="69091-601">Example claims mapping policies</span></span>

<span data-ttu-id="69091-602">Azure AD에서 특정 서비스 주체에 대해 토큰에 내보내지는 클레임을 사용자 지정할 수 있는 경우 많은 시나리오가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-602">In Azure AD, many scenarios are possible when you can customize claims emitted in tokens for specific service principals.</span></span> <span data-ttu-id="69091-603">이 섹션에 살펴보기 toouse hello 매핑 정책 형식을 요구 하는 방법을 이해 하는 데 도움이 되는 몇 가지 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-603">In this section, we walk through a few common scenarios that can help you grasp how toouse hello claims mapping policy type.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="69091-604">필수 조건</span><span class="sxs-lookup"><span data-stu-id="69091-604">Prerequisites</span></span>
<span data-ttu-id="69091-605">다음 예제는 hello, 업데이트, 링크를 만들고 서비스 사용자에 대 한 정책을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-605">In hello following examples, you create, update, link, and delete policies for service principals.</span></span> <span data-ttu-id="69091-606">새 tooAzure AD 인 경우 Azure AD는 tooget 이러한 예제를 진행 하기 전에 테 넌 트에 대 한 자세한 내용은 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-606">If you are new tooAzure AD, we recommend that you learn about how tooget an Azure AD tenant before you proceed with these examples.</span></span> 

<span data-ttu-id="69091-607">시작 tooget 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-607">tooget started, do hello following steps:</span></span>


1. <span data-ttu-id="69091-608">Hello를 최신 버전 다운로드 [Azure AD PowerShell 모듈 공개 미리 보기 릴리스에서](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127)합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-608">Download hello latest [Azure AD PowerShell Module public preview release](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).</span></span>
2.  <span data-ttu-id="69091-609">Hello Connect 명령 toosign tooyour Azure AD 관리자 계정에서에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-609">Run hello Connect command toosign in tooyour Azure AD admin account.</span></span> <span data-ttu-id="69091-610">새 세션을 시작할 때마다 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-610">Run this command each time you start a new session.</span></span>
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  <span data-ttu-id="69091-611">toosee 다음 실행된 hello 조직에서 생성 된 모든 정책을 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="69091-611">toosee all policies that have been created in your organization, run hello following command.</span></span> <span data-ttu-id="69091-612">Hello에 대부분의 작업 후이 명령을 실행 하는 것이 좋습니다 toocheck 정책으로 만들고 있는 다음 시나리오를 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-612">We recommend that you run this command after most operations in hello following scenarios, toocheck that your policies are being created as expected.</span></span>
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a><span data-ttu-id="69091-613">예:가 만들고는 정책 tooomit hello 기본의 클레임을 발급 한 토큰 tooa 서비스 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-613">Example: Create and assign a policy tooomit hello basic claims from tokens issued tooa service principal.</span></span>
<span data-ttu-id="69091-614">이 예제에서 발급 한 토큰 toolinked hello 기본 클레임 집합을 제거 하는 정책을 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69091-614">In this example, you create a policy that removes hello basic claim set from tokens issued toolinked service principals.</span></span>


1. <span data-ttu-id="69091-615">클레임 매핑 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69091-615">Create a claims mapping policy.</span></span> <span data-ttu-id="69091-616">이 정책에 연결 된 toospecific 서비스 보안 주체 토큰에서 hello 기본 클레임 집합을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-616">This policy, linked toospecific service principals, removes hello basic claim set from tokens.</span></span>
    1. <span data-ttu-id="69091-617">이 명령을 실행 toocreate hello 정책:</span><span class="sxs-lookup"><span data-stu-id="69091-617">toocreate hello policy, run this command:</span></span> 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. <span data-ttu-id="69091-618">새 정책 및 tooget hello 정책 ObjectId, 다음 실행된 hello 명령을 toosee:</span><span class="sxs-lookup"><span data-stu-id="69091-618">toosee your new policy, and tooget hello policy ObjectId, run hello following command:</span></span>
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="69091-619">Hello 정책 tooyour 서비스 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-619">Assign hello policy tooyour service principal.</span></span> <span data-ttu-id="69091-620">서비스 사용자의 ObjectId tooget hello를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-620">You also need tooget hello ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="69091-621">toosee 조직의 모든 서비스 사용자를 Microsoft Graph를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-621">toosee all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="69091-622">또는 Azure AD 그래프 탐색기에서 tooyour Azure AD 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-622">Or, in Azure AD Graph Explorer, sign in tooyour Azure AD account.</span></span>
    2.  <span data-ttu-id="69091-623">다음 명령을 하 여 서비스 보안 주체를 실행 hello의 ObjectId hello을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-623">When you have hello ObjectId of your service principal, run hello following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a><span data-ttu-id="69091-624">예: 만들기 및 정책 tooinclude 할당 토큰의에서 클레임을 발급 tooa 서비스 사용자 EmployeeID 및 TenantCountry hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-624">Example: Create and assign a policy tooinclude hello EmployeeID and TenantCountry as claims in tokens issued tooa service principal.</span></span>
<span data-ttu-id="69091-625">이 예제에서는 hello EmployeeID를 추가 하는 정책을 만들고 TenantCountry tootokens toolinked 서비스 보안 주체를 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-625">In this example, you create a policy that adds hello EmployeeID and TenantCountry tootokens issued toolinked service principals.</span></span> <span data-ttu-id="69091-626">hello EmployeeID는 SAML 토큰 및 Jwt 모두에서 hello 이름 클레임 유형으로 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="69091-626">hello EmployeeID is emitted as hello name claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="69091-627">hello TenantCountry hello 국가 클레임 SAML 토큰과 Jwt에 형식으로 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="69091-627">hello TenantCountry is emitted as hello country claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="69091-628">이 예제에서는 hello 토큰에 설정할 tooinclude hello basic 요구를 계속 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-628">In this example, we continue tooinclude hello basic claims set in hello tokens.</span></span>

1. <span data-ttu-id="69091-629">클레임 매핑 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69091-629">Create a claims mapping policy.</span></span> <span data-ttu-id="69091-630">이 정책에 연결 된 toospecific 서비스 사용자는 hello EmployeeID 및 TenantCountry 클레임 tootokens를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-630">This policy, linked toospecific service principals, adds hello EmployeeID and TenantCountry claims tootokens.</span></span>
    1. <span data-ttu-id="69091-631">이 명령을 실행 toocreate hello 정책:</span><span class="sxs-lookup"><span data-stu-id="69091-631">toocreate hello policy, run this command:</span></span>  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. <span data-ttu-id="69091-632">새 정책 및 tooget hello 정책 ObjectId, 다음 실행된 hello 명령을 toosee:</span><span class="sxs-lookup"><span data-stu-id="69091-632">toosee your new policy, and tooget hello policy ObjectId, run hello following command:</span></span>
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="69091-633">Hello 정책 tooyour 서비스 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-633">Assign hello policy tooyour service principal.</span></span> <span data-ttu-id="69091-634">서비스 사용자의 ObjectId tooget hello를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-634">You also need tooget hello ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="69091-635">toosee 조직의 모든 서비스 사용자를 Microsoft Graph를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-635">toosee all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="69091-636">또는 Azure AD 그래프 탐색기에서 tooyour Azure AD 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-636">Or, in Azure AD Graph Explorer, sign in tooyour Azure AD account.</span></span>
    2.  <span data-ttu-id="69091-637">다음 명령을 하 여 서비스 보안 주체를 실행 hello의 ObjectId hello을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-637">When you have hello ObjectId of your service principal, run hello following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a><span data-ttu-id="69091-638">예: 만들기 및 발급 된 토큰 tooa 서비스 사용자에 클레임 변환을 사용 하는 정책을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-638">Example: Create and assign a policy that uses a claims transformation in tokens issued tooa service principal.</span></span>
<span data-ttu-id="69091-639">이 예제에서는 내보내는 사용자 지정 클레임 "JoinedData" tooJWTs toolinked 서비스 보안 주체를 발급 하는 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-639">In this example, you create a policy that emits a custom claim “JoinedData” tooJWTs issued toolinked service principals.</span></span> <span data-ttu-id="69091-640">이 클레임 ".sandbox" 인 hello 사용자 개체에 hello extensionattribute1 특성에 저장 된 hello 데이터를 조인 하 여 만든 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-640">This claim contains a value created by joining hello data stored in hello extensionattribute1 attribute on hello user object with “.sandbox”.</span></span> <span data-ttu-id="69091-641">이 예제에서는 hello 토큰에 설정 하는 hello 기본 클레임을 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-641">In this example, we exclude hello basic claims set in hello tokens.</span></span>


1. <span data-ttu-id="69091-642">클레임 매핑 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69091-642">Create a claims mapping policy.</span></span> <span data-ttu-id="69091-643">이 정책에 연결 된 toospecific 서비스 사용자는 hello EmployeeID 및 TenantCountry 클레임 tootokens를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-643">This policy, linked toospecific service principals, adds hello EmployeeID and TenantCountry claims tootokens.</span></span>
    1. <span data-ttu-id="69091-644">이 명령을 실행 toocreate hello 정책:</span><span class="sxs-lookup"><span data-stu-id="69091-644">toocreate hello policy, run this command:</span></span> 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. <span data-ttu-id="69091-645">새 정책 및 tooget hello 정책 ObjectId, 다음 실행된 hello 명령을 toosee:</span><span class="sxs-lookup"><span data-stu-id="69091-645">toosee your new policy, and tooget hello policy ObjectId, run hello following command:</span></span> 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="69091-646">Hello 정책 tooyour 서비스 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-646">Assign hello policy tooyour service principal.</span></span> <span data-ttu-id="69091-647">서비스 사용자의 ObjectId tooget hello를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-647">You also need tooget hello ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="69091-648">toosee 조직의 모든 서비스 사용자를 Microsoft Graph를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-648">toosee all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="69091-649">또는 Azure AD 그래프 탐색기에서 tooyour Azure AD 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69091-649">Or, in Azure AD Graph Explorer, sign in tooyour Azure AD account.</span></span>
    2.  <span data-ttu-id="69091-650">다음 명령을 하 여 서비스 보안 주체를 실행 hello의 ObjectId hello을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69091-650">When you have hello ObjectId of your service principal, run hello following command:</span></span> 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
