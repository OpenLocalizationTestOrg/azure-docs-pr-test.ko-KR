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
ms.openlocfilehash: 78dbbe085fca26ad529c6262ba852f3c06ace404
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a><span data-ttu-id="c4320-103">Azure Active Directory의 클레임 매핑(공개 미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c4320-103">Claims mapping in Azure Active Directory (public preview)</span></span>

>[!NOTE]
><span data-ttu-id="c4320-104">이 기능은 현재 포털을 통해 제공되는 [클레임 사용자 지정](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization)을 바꾸고 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-104">This feature replaces and supersedes the [claims customization](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) offered through the portal today.</span></span> <span data-ttu-id="c4320-105">이 문서에 자세히 설명된 Graph/PowerShell 방법뿐만 아니라 포털을 사용하여 동일한 응용 프로그램에서 클레임을 사용자 지정하는 경우 해당 응용 프로그램에 발급된 토큰은 포털의 구성을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-105">If you customize claims using the portal in addition to the Graph/PowerShell method detailed in this document on the same application, tokens issued for that application will ignore the configuration in the portal.</span></span>
<span data-ttu-id="c4320-106">이 문서에 설명된 방법을 통해 만들어진 구성은 포털에서 반영되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-106">Configurations made through the methods detailed in this document will not be reflected in the portal.</span></span>

<span data-ttu-id="c4320-107">이 기능은 테넌트 관리자가 테넌트의 특정 응용 프로그램에 대한 토큰에 내보내지는 클레임을 사용자 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-107">This feature is used by tenant admins to customize the claims emitted in tokens for a specific application in their tenant.</span></span> <span data-ttu-id="c4320-108">다음과 같은 경우 클레임 매핑 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-108">You can use claims mapping policies to:</span></span>

- <span data-ttu-id="c4320-109">토큰에 포함할 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-109">Select which claims are included in tokens.</span></span>
- <span data-ttu-id="c4320-110">아직 존재하지 않는 클레임 형식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-110">Create claim types that do not already exist.</span></span>
- <span data-ttu-id="c4320-111">특정 클레임에 내보내지는 데이터 원본을 선택하거나 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-111">Choose or change the source of data emitted in specific claims.</span></span>

>[!NOTE]
><span data-ttu-id="c4320-112">이 기능은 현재 공개 미리 보기로 제공되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-112">This capability currently is in public preview.</span></span> <span data-ttu-id="c4320-113">변경 내용을 되돌리거나 제거할 준비를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-113">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="c4320-114">이 기능은 공개 미리 보기 동안 모든 Azure AD(Azure Active Directory) 구독에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-114">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="c4320-115">그러나 기능이 일반 공급되면 일부 기능에는 Azure Active Directory Premium 구독이 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-115">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span>

## <a name="claims-mapping-policy-type"></a><span data-ttu-id="c4320-116">클레임 매핑 정책 유형</span><span class="sxs-lookup"><span data-stu-id="c4320-116">Claims mapping policy type</span></span>
<span data-ttu-id="c4320-117">Azure AD에서 **정책** 개체는 조직에 있는 개별 응용 프로그램 또는 모든 응용 프로그램에 적용되는 규칙 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-117">In Azure AD, a **Policy** object represents a set of rules enforced on individual applications, or on all applications in an organization.</span></span> <span data-ttu-id="c4320-118">각 유형의 정책에는 할당된 개체에 적용되는 속성 집합이 포함된 고유한 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-118">Each type of policy has a unique structure, with a set of properties that are then applied to objects to which they are assigned.</span></span>

<span data-ttu-id="c4320-119">클레임 매핑 정책은 특정 응용 프로그램에 대해 발급된 토큰에 내보내지는 클레임을 수정하는 **정책** 개체의 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-119">A claims mapping policy is a type of **Policy** object that modifies the claims emitted in tokens issued for specific applications.</span></span>

## <a name="claim-sets"></a><span data-ttu-id="c4320-120">클레임 집합</span><span class="sxs-lookup"><span data-stu-id="c4320-120">Claim sets</span></span>
<span data-ttu-id="c4320-121">토큰에 사용되는 시기와 방법을 정의하는 특정 클레임 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-121">There are certain sets of claims that define how and when they are used in tokens.</span></span>

### <a name="core-claim-set"></a><span data-ttu-id="c4320-122">핵심 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="c4320-122">Core claim set</span></span>
<span data-ttu-id="c4320-123">핵심 클레임 집합의 클레임은 정책에 관계없이 모든 토큰에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-123">Claims in the core claim set are present in every token, regardless of policy.</span></span> <span data-ttu-id="c4320-124">또한 이러한 클레임은 제한된 것으로 간주되며 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-124">These claims are also considered restricted, and cannot be modified.</span></span>

### <a name="basic-claim-set"></a><span data-ttu-id="c4320-125">기본 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="c4320-125">Basic claim set</span></span>
<span data-ttu-id="c4320-126">기본 클레임 집합에는 핵심 클레임 집합뿐 아니라 토큰에 대해 기본적으로 내보내지는 클레임을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-126">The basic claim set includes the claims that are emitted by default for tokens (in addition to the core claim set).</span></span> <span data-ttu-id="c4320-127">클레임 매핑 정책을 사용하여 이러한 클레임을 생략하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-127">These claims can be omitted or modified by using the claims mapping policies.</span></span>

### <a name="restricted-claim-set"></a><span data-ttu-id="c4320-128">제한된 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="c4320-128">Restricted claim set</span></span>
<span data-ttu-id="c4320-129">정책을 사용하여 제한된 클레임을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-129">Restricted claims cannot be modified by using policy.</span></span> <span data-ttu-id="c4320-130">데이터 원본을 변경할 수 없으며, 이러한 클레임을 생성할 때 변환이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-130">The data source cannot be changed, and no transformation is applied when generating these claims.</span></span>

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a><span data-ttu-id="c4320-131">표 1: JWT(JSON Web Token) 제한된 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="c4320-131">Table 1: JSON Web Token (JWT) restricted claim set</span></span>
|<span data-ttu-id="c4320-132">클레임 형식(이름)</span><span class="sxs-lookup"><span data-stu-id="c4320-132">Claim type (name)</span></span>|
| ----- |
|<span data-ttu-id="c4320-133">_claim_names</span><span class="sxs-lookup"><span data-stu-id="c4320-133">_claim_names</span></span>|
|<span data-ttu-id="c4320-134">_claim_sources</span><span class="sxs-lookup"><span data-stu-id="c4320-134">_claim_sources</span></span>|
|<span data-ttu-id="c4320-135">access_token</span><span class="sxs-lookup"><span data-stu-id="c4320-135">access_token</span></span>|
|<span data-ttu-id="c4320-136">account_type</span><span class="sxs-lookup"><span data-stu-id="c4320-136">account_type</span></span>|
|<span data-ttu-id="c4320-137">acr</span><span class="sxs-lookup"><span data-stu-id="c4320-137">acr</span></span>|
|<span data-ttu-id="c4320-138">actor</span><span class="sxs-lookup"><span data-stu-id="c4320-138">actor</span></span>|
|<span data-ttu-id="c4320-139">actortoken</span><span class="sxs-lookup"><span data-stu-id="c4320-139">actortoken</span></span>|
|<span data-ttu-id="c4320-140">aio</span><span class="sxs-lookup"><span data-stu-id="c4320-140">aio</span></span>|
|<span data-ttu-id="c4320-141">altsecid</span><span class="sxs-lookup"><span data-stu-id="c4320-141">altsecid</span></span>|
|<span data-ttu-id="c4320-142">amr</span><span class="sxs-lookup"><span data-stu-id="c4320-142">amr</span></span>|
|<span data-ttu-id="c4320-143">app_chain</span><span class="sxs-lookup"><span data-stu-id="c4320-143">app_chain</span></span>|
|<span data-ttu-id="c4320-144">app_displayname</span><span class="sxs-lookup"><span data-stu-id="c4320-144">app_displayname</span></span>|
|<span data-ttu-id="c4320-145">app_res</span><span class="sxs-lookup"><span data-stu-id="c4320-145">app_res</span></span>|
|<span data-ttu-id="c4320-146">appctx</span><span class="sxs-lookup"><span data-stu-id="c4320-146">appctx</span></span>|
|<span data-ttu-id="c4320-147">appctxsender</span><span class="sxs-lookup"><span data-stu-id="c4320-147">appctxsender</span></span>|
|<span data-ttu-id="c4320-148">appId</span><span class="sxs-lookup"><span data-stu-id="c4320-148">appid</span></span>|
|<span data-ttu-id="c4320-149">appidacr</span><span class="sxs-lookup"><span data-stu-id="c4320-149">appidacr</span></span>|
|<span data-ttu-id="c4320-150">어설션</span><span class="sxs-lookup"><span data-stu-id="c4320-150">assertion</span></span>|
|<span data-ttu-id="c4320-151">at_hash</span><span class="sxs-lookup"><span data-stu-id="c4320-151">at_hash</span></span>|
|<span data-ttu-id="c4320-152">aud</span><span class="sxs-lookup"><span data-stu-id="c4320-152">aud</span></span>|
|<span data-ttu-id="c4320-153">auth_data</span><span class="sxs-lookup"><span data-stu-id="c4320-153">auth_data</span></span>|
|<span data-ttu-id="c4320-154">auth_time</span><span class="sxs-lookup"><span data-stu-id="c4320-154">auth_time</span></span>|
|<span data-ttu-id="c4320-155">authorization_code</span><span class="sxs-lookup"><span data-stu-id="c4320-155">authorization_code</span></span>|
|<span data-ttu-id="c4320-156">azp</span><span class="sxs-lookup"><span data-stu-id="c4320-156">azp</span></span>|
|<span data-ttu-id="c4320-157">azpacr</span><span class="sxs-lookup"><span data-stu-id="c4320-157">azpacr</span></span>|
|<span data-ttu-id="c4320-158">c_hash</span><span class="sxs-lookup"><span data-stu-id="c4320-158">c_hash</span></span>|
|<span data-ttu-id="c4320-159">ca_enf</span><span class="sxs-lookup"><span data-stu-id="c4320-159">ca_enf</span></span>|
|<span data-ttu-id="c4320-160">cc</span><span class="sxs-lookup"><span data-stu-id="c4320-160">cc</span></span>|
|<span data-ttu-id="c4320-161">cert_token_use</span><span class="sxs-lookup"><span data-stu-id="c4320-161">cert_token_use</span></span>|
|<span data-ttu-id="c4320-162">client_id</span><span class="sxs-lookup"><span data-stu-id="c4320-162">client_id</span></span>|
|<span data-ttu-id="c4320-163">cloud_graph_host_name</span><span class="sxs-lookup"><span data-stu-id="c4320-163">cloud_graph_host_name</span></span>|
|<span data-ttu-id="c4320-164">cloud_instance_name</span><span class="sxs-lookup"><span data-stu-id="c4320-164">cloud_instance_name</span></span>|
|<span data-ttu-id="c4320-165">cnf</span><span class="sxs-lookup"><span data-stu-id="c4320-165">cnf</span></span>|
|<span data-ttu-id="c4320-166">코드</span><span class="sxs-lookup"><span data-stu-id="c4320-166">code</span></span>|
|<span data-ttu-id="c4320-167">controls</span><span class="sxs-lookup"><span data-stu-id="c4320-167">controls</span></span>|
|<span data-ttu-id="c4320-168">credential_keys</span><span class="sxs-lookup"><span data-stu-id="c4320-168">credential_keys</span></span>|
|<span data-ttu-id="c4320-169">csr</span><span class="sxs-lookup"><span data-stu-id="c4320-169">csr</span></span>|
|<span data-ttu-id="c4320-170">csr_type</span><span class="sxs-lookup"><span data-stu-id="c4320-170">csr_type</span></span>|
|<span data-ttu-id="c4320-171">deviceId</span><span class="sxs-lookup"><span data-stu-id="c4320-171">deviceid</span></span>|
|<span data-ttu-id="c4320-172">dns_names</span><span class="sxs-lookup"><span data-stu-id="c4320-172">dns_names</span></span>|
|<span data-ttu-id="c4320-173">domain_dns_name</span><span class="sxs-lookup"><span data-stu-id="c4320-173">domain_dns_name</span></span>|
|<span data-ttu-id="c4320-174">domain_netbios_name</span><span class="sxs-lookup"><span data-stu-id="c4320-174">domain_netbios_name</span></span>|
|<span data-ttu-id="c4320-175">e_exp</span><span class="sxs-lookup"><span data-stu-id="c4320-175">e_exp</span></span>|
|<span data-ttu-id="c4320-176">email</span><span class="sxs-lookup"><span data-stu-id="c4320-176">email</span></span>|
|<span data-ttu-id="c4320-177">endpoint</span><span class="sxs-lookup"><span data-stu-id="c4320-177">endpoint</span></span>|
|<span data-ttu-id="c4320-178">enfpolids</span><span class="sxs-lookup"><span data-stu-id="c4320-178">enfpolids</span></span>|
|<span data-ttu-id="c4320-179">exp</span><span class="sxs-lookup"><span data-stu-id="c4320-179">exp</span></span>|
|<span data-ttu-id="c4320-180">expires_on</span><span class="sxs-lookup"><span data-stu-id="c4320-180">expires_on</span></span>|
|<span data-ttu-id="c4320-181">grant_type</span><span class="sxs-lookup"><span data-stu-id="c4320-181">grant_type</span></span>|
|<span data-ttu-id="c4320-182">graph</span><span class="sxs-lookup"><span data-stu-id="c4320-182">graph</span></span>|
|<span data-ttu-id="c4320-183">group_sids</span><span class="sxs-lookup"><span data-stu-id="c4320-183">group_sids</span></span>|
|<span data-ttu-id="c4320-184">groups</span><span class="sxs-lookup"><span data-stu-id="c4320-184">groups</span></span>|
|<span data-ttu-id="c4320-185">hasgroups</span><span class="sxs-lookup"><span data-stu-id="c4320-185">hasgroups</span></span>|
|<span data-ttu-id="c4320-186">hash_alg</span><span class="sxs-lookup"><span data-stu-id="c4320-186">hash_alg</span></span>|
|<span data-ttu-id="c4320-187">home_oid</span><span class="sxs-lookup"><span data-stu-id="c4320-187">home_oid</span></span>|
|<span data-ttu-id="c4320-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="c4320-188">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span>|
|<span data-ttu-id="c4320-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="c4320-189">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span>|
|<span data-ttu-id="c4320-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="c4320-190">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span>|
|<span data-ttu-id="c4320-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="c4320-191">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span>|
|<span data-ttu-id="c4320-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="c4320-192">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span>|
|<span data-ttu-id="c4320-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name</span><span class="sxs-lookup"><span data-stu-id="c4320-193">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name</span></span>|
|<span data-ttu-id="c4320-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier</span><span class="sxs-lookup"><span data-stu-id="c4320-194">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier</span></span>|
|<span data-ttu-id="c4320-195">iat</span><span class="sxs-lookup"><span data-stu-id="c4320-195">iat</span></span>|
|<span data-ttu-id="c4320-196">identityprovider</span><span class="sxs-lookup"><span data-stu-id="c4320-196">identityprovider</span></span>|
|<span data-ttu-id="c4320-197">idp</span><span class="sxs-lookup"><span data-stu-id="c4320-197">idp</span></span>|
|<span data-ttu-id="c4320-198">in_corp</span><span class="sxs-lookup"><span data-stu-id="c4320-198">in_corp</span></span>|
|<span data-ttu-id="c4320-199">instance</span><span class="sxs-lookup"><span data-stu-id="c4320-199">instance</span></span>|
|<span data-ttu-id="c4320-200">ipaddr</span><span class="sxs-lookup"><span data-stu-id="c4320-200">ipaddr</span></span>|
|<span data-ttu-id="c4320-201">isbrowserhostedapp</span><span class="sxs-lookup"><span data-stu-id="c4320-201">isbrowserhostedapp</span></span>|
|<span data-ttu-id="c4320-202">iss</span><span class="sxs-lookup"><span data-stu-id="c4320-202">iss</span></span>|
|<span data-ttu-id="c4320-203">jwk</span><span class="sxs-lookup"><span data-stu-id="c4320-203">jwk</span></span>|
|<span data-ttu-id="c4320-204">key_id</span><span class="sxs-lookup"><span data-stu-id="c4320-204">key_id</span></span>|
|<span data-ttu-id="c4320-205">key_type</span><span class="sxs-lookup"><span data-stu-id="c4320-205">key_type</span></span>|
|<span data-ttu-id="c4320-206">mam_compliance_url</span><span class="sxs-lookup"><span data-stu-id="c4320-206">mam_compliance_url</span></span>|
|<span data-ttu-id="c4320-207">mam_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="c4320-207">mam_enrollment_url</span></span>|
|<span data-ttu-id="c4320-208">mam_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="c4320-208">mam_terms_of_use_url</span></span>|
|<span data-ttu-id="c4320-209">mdm_compliance_url</span><span class="sxs-lookup"><span data-stu-id="c4320-209">mdm_compliance_url</span></span>|
|<span data-ttu-id="c4320-210">mdm_enrollment_url</span><span class="sxs-lookup"><span data-stu-id="c4320-210">mdm_enrollment_url</span></span>|
|<span data-ttu-id="c4320-211">mdm_terms_of_use_url</span><span class="sxs-lookup"><span data-stu-id="c4320-211">mdm_terms_of_use_url</span></span>|
|<span data-ttu-id="c4320-212">nameid</span><span class="sxs-lookup"><span data-stu-id="c4320-212">nameid</span></span>|
|<span data-ttu-id="c4320-213">nbf</span><span class="sxs-lookup"><span data-stu-id="c4320-213">nbf</span></span>|
|<span data-ttu-id="c4320-214">netbios_name</span><span class="sxs-lookup"><span data-stu-id="c4320-214">netbios_name</span></span>|
|<span data-ttu-id="c4320-215">nonce</span><span class="sxs-lookup"><span data-stu-id="c4320-215">nonce</span></span>|
|<span data-ttu-id="c4320-216">oid</span><span class="sxs-lookup"><span data-stu-id="c4320-216">oid</span></span>|
|<span data-ttu-id="c4320-217">on_prem_id</span><span class="sxs-lookup"><span data-stu-id="c4320-217">on_prem_id</span></span>|
|<span data-ttu-id="c4320-218">onprem_sam_account_name</span><span class="sxs-lookup"><span data-stu-id="c4320-218">onprem_sam_account_name</span></span>|
|<span data-ttu-id="c4320-219">onprem_sid</span><span class="sxs-lookup"><span data-stu-id="c4320-219">onprem_sid</span></span>|
|<span data-ttu-id="c4320-220">openid2_id</span><span class="sxs-lookup"><span data-stu-id="c4320-220">openid2_id</span></span>|
|<span data-ttu-id="c4320-221">password</span><span class="sxs-lookup"><span data-stu-id="c4320-221">password</span></span>|
|<span data-ttu-id="c4320-222">platf</span><span class="sxs-lookup"><span data-stu-id="c4320-222">platf</span></span>|
|<span data-ttu-id="c4320-223">polids</span><span class="sxs-lookup"><span data-stu-id="c4320-223">polids</span></span>|
|<span data-ttu-id="c4320-224">pop_jwk</span><span class="sxs-lookup"><span data-stu-id="c4320-224">pop_jwk</span></span>|
|<span data-ttu-id="c4320-225">preferred_username</span><span class="sxs-lookup"><span data-stu-id="c4320-225">preferred_username</span></span>|
|<span data-ttu-id="c4320-226">previous_refresh_token</span><span class="sxs-lookup"><span data-stu-id="c4320-226">previous_refresh_token</span></span>|
|<span data-ttu-id="c4320-227">primary_sid</span><span class="sxs-lookup"><span data-stu-id="c4320-227">primary_sid</span></span>|
|<span data-ttu-id="c4320-228">puid</span><span class="sxs-lookup"><span data-stu-id="c4320-228">puid</span></span>|
|<span data-ttu-id="c4320-229">pwd_exp</span><span class="sxs-lookup"><span data-stu-id="c4320-229">pwd_exp</span></span>|
|<span data-ttu-id="c4320-230">pwd_url</span><span class="sxs-lookup"><span data-stu-id="c4320-230">pwd_url</span></span>|
|<span data-ttu-id="c4320-231">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="c4320-231">redirect_uri</span></span>|
|<span data-ttu-id="c4320-232">refresh_token</span><span class="sxs-lookup"><span data-stu-id="c4320-232">refresh_token</span></span>|
|<span data-ttu-id="c4320-233">refreshtoken</span><span class="sxs-lookup"><span data-stu-id="c4320-233">refreshtoken</span></span>|
|<span data-ttu-id="c4320-234">request_nonce</span><span class="sxs-lookup"><span data-stu-id="c4320-234">request_nonce</span></span>|
|<span data-ttu-id="c4320-235">resource</span><span class="sxs-lookup"><span data-stu-id="c4320-235">resource</span></span>|
|<span data-ttu-id="c4320-236">role</span><span class="sxs-lookup"><span data-stu-id="c4320-236">role</span></span>|
|<span data-ttu-id="c4320-237">roles</span><span class="sxs-lookup"><span data-stu-id="c4320-237">roles</span></span>|
|<span data-ttu-id="c4320-238">scope</span><span class="sxs-lookup"><span data-stu-id="c4320-238">scope</span></span>|
|<span data-ttu-id="c4320-239">scp</span><span class="sxs-lookup"><span data-stu-id="c4320-239">scp</span></span>|
|<span data-ttu-id="c4320-240">sid</span><span class="sxs-lookup"><span data-stu-id="c4320-240">sid</span></span>|
|<span data-ttu-id="c4320-241">signature</span><span class="sxs-lookup"><span data-stu-id="c4320-241">signature</span></span>|
|<span data-ttu-id="c4320-242">signin_state</span><span class="sxs-lookup"><span data-stu-id="c4320-242">signin_state</span></span>|
|<span data-ttu-id="c4320-243">src1</span><span class="sxs-lookup"><span data-stu-id="c4320-243">src1</span></span>|
|<span data-ttu-id="c4320-244">src2</span><span class="sxs-lookup"><span data-stu-id="c4320-244">src2</span></span>|
|<span data-ttu-id="c4320-245">sub</span><span class="sxs-lookup"><span data-stu-id="c4320-245">sub</span></span>|
|<span data-ttu-id="c4320-246">tbid</span><span class="sxs-lookup"><span data-stu-id="c4320-246">tbid</span></span>|
|<span data-ttu-id="c4320-247">tenant_display_name</span><span class="sxs-lookup"><span data-stu-id="c4320-247">tenant_display_name</span></span>|
|<span data-ttu-id="c4320-248">tenant_region_scope</span><span class="sxs-lookup"><span data-stu-id="c4320-248">tenant_region_scope</span></span>|
|<span data-ttu-id="c4320-249">thumbnail_photo</span><span class="sxs-lookup"><span data-stu-id="c4320-249">thumbnail_photo</span></span>|
|<span data-ttu-id="c4320-250">tid</span><span class="sxs-lookup"><span data-stu-id="c4320-250">tid</span></span>|
|<span data-ttu-id="c4320-251">tokenAutologonEnabled</span><span class="sxs-lookup"><span data-stu-id="c4320-251">tokenAutologonEnabled</span></span>|
|<span data-ttu-id="c4320-252">trustedfordelegation</span><span class="sxs-lookup"><span data-stu-id="c4320-252">trustedfordelegation</span></span>|
|<span data-ttu-id="c4320-253">unique_name</span><span class="sxs-lookup"><span data-stu-id="c4320-253">unique_name</span></span>|
|<span data-ttu-id="c4320-254">upn</span><span class="sxs-lookup"><span data-stu-id="c4320-254">upn</span></span>|
|<span data-ttu-id="c4320-255">user_setting_sync_url</span><span class="sxs-lookup"><span data-stu-id="c4320-255">user_setting_sync_url</span></span>|
|<span data-ttu-id="c4320-256">username</span><span class="sxs-lookup"><span data-stu-id="c4320-256">username</span></span>|
|<span data-ttu-id="c4320-257">uti</span><span class="sxs-lookup"><span data-stu-id="c4320-257">uti</span></span>|
|<span data-ttu-id="c4320-258">ver</span><span class="sxs-lookup"><span data-stu-id="c4320-258">ver</span></span>|
|<span data-ttu-id="c4320-259">verified_primary_email</span><span class="sxs-lookup"><span data-stu-id="c4320-259">verified_primary_email</span></span>|
|<span data-ttu-id="c4320-260">verified_secondary_email</span><span class="sxs-lookup"><span data-stu-id="c4320-260">verified_secondary_email</span></span>|
|<span data-ttu-id="c4320-261">wids</span><span class="sxs-lookup"><span data-stu-id="c4320-261">wids</span></span>|
|<span data-ttu-id="c4320-262">win_ver</span><span class="sxs-lookup"><span data-stu-id="c4320-262">win_ver</span></span>|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a><span data-ttu-id="c4320-263">표 2: SAML(Security Assertion Markup Language) 제한된 클레임 집합</span><span class="sxs-lookup"><span data-stu-id="c4320-263">Table 2: Security Assertion Markup Language (SAML) restricted claim set</span></span>
|<span data-ttu-id="c4320-264">클레임 형식(URI)</span><span class="sxs-lookup"><span data-stu-id="c4320-264">Claim type (URI)</span></span>|
| ----- |
|<span data-ttu-id="c4320-265">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span><span class="sxs-lookup"><span data-stu-id="c4320-265">http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration</span></span>|
|<span data-ttu-id="c4320-266">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span><span class="sxs-lookup"><span data-stu-id="c4320-266">http://schemas.microsoft.com/ws/2008/06/identity/claims/expired</span></span>|
|<span data-ttu-id="c4320-267">http://schemas.microsoft.com/identity/claims/accesstoken</span><span class="sxs-lookup"><span data-stu-id="c4320-267">http://schemas.microsoft.com/identity/claims/accesstoken</span></span>|
|<span data-ttu-id="c4320-268">http://schemas.microsoft.com/identity/claims/openid2_id</span><span class="sxs-lookup"><span data-stu-id="c4320-268">http://schemas.microsoft.com/identity/claims/openid2_id</span></span>|
|<span data-ttu-id="c4320-269">http://schemas.microsoft.com/identity/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="c4320-269">http://schemas.microsoft.com/identity/claims/identityprovider</span></span>|
|<span data-ttu-id="c4320-270">http://schemas.microsoft.com/identity/claims/objectidentifier</span><span class="sxs-lookup"><span data-stu-id="c4320-270">http://schemas.microsoft.com/identity/claims/objectidentifier</span></span>|
|<span data-ttu-id="c4320-271">http://schemas.microsoft.com/identity/claims/puid</span><span class="sxs-lookup"><span data-stu-id="c4320-271">http://schemas.microsoft.com/identity/claims/puid</span></span>|
|<span data-ttu-id="c4320-272">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span><span class="sxs-lookup"><span data-stu-id="c4320-272">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1]</span></span> |
|<span data-ttu-id="c4320-273">http://schemas.microsoft.com/identity/claims/tenantid</span><span class="sxs-lookup"><span data-stu-id="c4320-273">http://schemas.microsoft.com/identity/claims/tenantid</span></span>|
|<span data-ttu-id="c4320-274">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span><span class="sxs-lookup"><span data-stu-id="c4320-274">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant</span></span>|
|<span data-ttu-id="c4320-275">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span><span class="sxs-lookup"><span data-stu-id="c4320-275">http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod</span></span>|
|<span data-ttu-id="c4320-276">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span><span class="sxs-lookup"><span data-stu-id="c4320-276">http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider</span></span>|
|<span data-ttu-id="c4320-277">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span><span class="sxs-lookup"><span data-stu-id="c4320-277">http://schemas.microsoft.com/ws/2008/06/identity/claims/groups</span></span>|
|<span data-ttu-id="c4320-278">http://schemas.microsoft.com/claims/groups.link</span><span class="sxs-lookup"><span data-stu-id="c4320-278">http://schemas.microsoft.com/claims/groups.link</span></span>|
|<span data-ttu-id="c4320-279">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span><span class="sxs-lookup"><span data-stu-id="c4320-279">http://schemas.microsoft.com/ws/2008/06/identity/claims/role</span></span>|
|<span data-ttu-id="c4320-280">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span><span class="sxs-lookup"><span data-stu-id="c4320-280">http://schemas.microsoft.com/ws/2008/06/identity/claims/wids</span></span>|
|<span data-ttu-id="c4320-281">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span><span class="sxs-lookup"><span data-stu-id="c4320-281">http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant</span></span>|
|<span data-ttu-id="c4320-282">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span><span class="sxs-lookup"><span data-stu-id="c4320-282">http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown</span></span>|
|<span data-ttu-id="c4320-283">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span><span class="sxs-lookup"><span data-stu-id="c4320-283">http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged</span></span>|
|<span data-ttu-id="c4320-284">http://schemas.microsoft.com/2014/03/psso</span><span class="sxs-lookup"><span data-stu-id="c4320-284">http://schemas.microsoft.com/2014/03/psso</span></span>|
|<span data-ttu-id="c4320-285">http://schemas.microsoft.com/claims/authnmethodsreferences</span><span class="sxs-lookup"><span data-stu-id="c4320-285">http://schemas.microsoft.com/claims/authnmethodsreferences</span></span>|
|<span data-ttu-id="c4320-286">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span><span class="sxs-lookup"><span data-stu-id="c4320-286">http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor</span></span>|
|<span data-ttu-id="c4320-287">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span><span class="sxs-lookup"><span data-stu-id="c4320-287">http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername</span></span>|
|<span data-ttu-id="c4320-288">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span><span class="sxs-lookup"><span data-stu-id="c4320-288">http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey</span></span>|
|<span data-ttu-id="c4320-289">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span><span class="sxs-lookup"><span data-stu-id="c4320-289">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname</span></span>|
|<span data-ttu-id="c4320-290">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span><span class="sxs-lookup"><span data-stu-id="c4320-290">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid</span></span>|
|<span data-ttu-id="c4320-291">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span><span class="sxs-lookup"><span data-stu-id="c4320-291">http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid</span></span>|
|<span data-ttu-id="c4320-292">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span><span class="sxs-lookup"><span data-stu-id="c4320-292">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision</span></span>|
|<span data-ttu-id="c4320-293">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span><span class="sxs-lookup"><span data-stu-id="c4320-293">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication</span></span>|
|<span data-ttu-id="c4320-294">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span><span class="sxs-lookup"><span data-stu-id="c4320-294">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid</span></span>|
|<span data-ttu-id="c4320-295">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span><span class="sxs-lookup"><span data-stu-id="c4320-295">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid</span></span>|
|<span data-ttu-id="c4320-296">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span><span class="sxs-lookup"><span data-stu-id="c4320-296">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid</span></span>|
|<span data-ttu-id="c4320-297">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span><span class="sxs-lookup"><span data-stu-id="c4320-297">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid</span></span>|
|<span data-ttu-id="c4320-298">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="c4320-298">http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup</span></span>|
|<span data-ttu-id="c4320-299">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span><span class="sxs-lookup"><span data-stu-id="c4320-299">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim</span></span>|
|<span data-ttu-id="c4320-300">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span><span class="sxs-lookup"><span data-stu-id="c4320-300">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup</span></span>|
|<span data-ttu-id="c4320-301">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span><span class="sxs-lookup"><span data-stu-id="c4320-301">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion</span></span>|
|<span data-ttu-id="c4320-302">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span><span class="sxs-lookup"><span data-stu-id="c4320-302">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority</span></span>|
|<span data-ttu-id="c4320-303">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span><span class="sxs-lookup"><span data-stu-id="c4320-303">http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim</span></span>|
|<span data-ttu-id="c4320-304">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span><span class="sxs-lookup"><span data-stu-id="c4320-304">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname</span></span>|
|<span data-ttu-id="c4320-305">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span><span class="sxs-lookup"><span data-stu-id="c4320-305">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn</span></span>|
|<span data-ttu-id="c4320-306">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span><span class="sxs-lookup"><span data-stu-id="c4320-306">http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid</span></span>|
|<span data-ttu-id="c4320-307">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span><span class="sxs-lookup"><span data-stu-id="c4320-307">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn</span></span>|
|<span data-ttu-id="c4320-308">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span><span class="sxs-lookup"><span data-stu-id="c4320-308">http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent</span></span>|
|<span data-ttu-id="c4320-309">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span><span class="sxs-lookup"><span data-stu-id="c4320-309">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier</span></span>|
|<span data-ttu-id="c4320-310">http://schemas.microsoft.com/identity/claims/scope</span><span class="sxs-lookup"><span data-stu-id="c4320-310">http://schemas.microsoft.com/identity/claims/scope</span></span>|

## <a name="claims-mapping-policy-properties"></a><span data-ttu-id="c4320-311">클레임 매핑 정책 속성</span><span class="sxs-lookup"><span data-stu-id="c4320-311">Claims mapping policy properties</span></span>
<span data-ttu-id="c4320-312">클레임 매핑 정책의 속성을 사용하여 내보내지는 클레임과 데이터가 소싱되는 위치를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-312">Use the properties of a claims mapping policy to control which claims are emitted, and where the data is sourced from.</span></span> <span data-ttu-id="c4320-313">정책을 설정하지 않으면 시스템은 핵심 클레임 집합, 기본 클레임 집합 및 응용 프로그램이 수신하도록 선택한 선택적 클레임이 포함된 토큰을 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-313">If no policy is set, the system issues tokens containing the core claim set, the basic claim set, and any optional claims that the application has chosen to receive.</span></span>

### <a name="include-basic-claim-set"></a><span data-ttu-id="c4320-314">기본 클레임 집합 포함</span><span class="sxs-lookup"><span data-stu-id="c4320-314">Include basic claim set</span></span>

<span data-ttu-id="c4320-315">**문자열:** IncludeBasicClaimSet</span><span class="sxs-lookup"><span data-stu-id="c4320-315">**String:** IncludeBasicClaimSet</span></span>

<span data-ttu-id="c4320-316">**데이터 형식:** 부울(True 또는 False)</span><span class="sxs-lookup"><span data-stu-id="c4320-316">**Data type:** Boolean (True or False)</span></span>

<span data-ttu-id="c4320-317">**요약:** 이 속성은 기본 클레임 집합이 이 정책의 영향을 받는 토큰에 포함되는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-317">**Summary:** This property determines whether the basic claim set is included in tokens affected by this policy.</span></span> 

- <span data-ttu-id="c4320-318">True로 설정된 경우 기본 클레임 집합의 모든 클레임이 정책의 영향을 받는 토큰에 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-318">If set to True, all claims in the basic claim set are emitted in tokens affected by the policy.</span></span> 
- <span data-ttu-id="c4320-319">False로 설정된 경우 기본 클레임 집합의 클레임은 동일한 정책의 클레임 스키마 속성에 개별적으로 추가되지 않는 한 토큰에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-319">If set to False, claims in the basic claim set are not in the tokens, unless they are individually added in the claims schema property of the same policy.</span></span>

>[!NOTE] 
><span data-ttu-id="c4320-320">핵심 클레임 집합의 클레임은 이 속성의 설정값에 관계없이 모든 토큰에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-320">Claims in the core claim set are present in every token, regardless of what this property is set to.</span></span> 

### <a name="claims-schema"></a><span data-ttu-id="c4320-321">클레임 스키마</span><span class="sxs-lookup"><span data-stu-id="c4320-321">Claims schema</span></span>

<span data-ttu-id="c4320-322">**문자열:** ClaimsSchema</span><span class="sxs-lookup"><span data-stu-id="c4320-322">**String:** ClaimsSchema</span></span>

<span data-ttu-id="c4320-323">**데이터 형식:** 하나 이상의 클레임 스키마 항목을 가진 JSON Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-323">**Data type:** JSON blob with one or more claim schema entries</span></span>

<span data-ttu-id="c4320-324">**요약:** 이 속성은 기본 클레임 집합 및 핵심 클레임 집합 외에도 정책의 영향을 받는 토큰에 표시될 클레임을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-324">**Summary:** This property defines which claims are present in the tokens affected by the policy, in addition to the basic claim set and the core claim set.</span></span>
<span data-ttu-id="c4320-325">이 속성에 정의된 각 클레임 스키마 항목의 경우 특정 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-325">For each claim schema entry defined in this property, certain information is required.</span></span> <span data-ttu-id="c4320-326">데이터가 제공되는 위치(**Value** 또는 **Source/ID 쌍**) 및 데이터를 내보내는 클레임(**클레임 유형**)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-326">You must specify where the data is coming from (**Value** or **Source/ID pair**), and which claim the data is emitted as (**Claim Type**).</span></span>

### <a name="claim-schema-entry-elements"></a><span data-ttu-id="c4320-327">클레임 스키마 항목 요소</span><span class="sxs-lookup"><span data-stu-id="c4320-327">Claim schema entry elements</span></span>

<span data-ttu-id="c4320-328">**값:** Value 요소는 클레임에 내보내지는 데이터로 정적 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-328">**Value:** The Value element defines a static value as the data to be emitted in the claim.</span></span>

<span data-ttu-id="c4320-329">**원본/ID 쌍:** Source 및 ID 요소는 클레임의 데이터가 제공되는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-329">**Source/ID pair:** The Source and ID elements define where the data in the claim is sourced from.</span></span> 

<span data-ttu-id="c4320-330">Source 요소는 다음 중 하나로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-330">The Source element must be set to one of the following:</span></span> 


- <span data-ttu-id="c4320-331">"user": 클레임의 데이터가 User 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-331">"user": The data in the claim is a property on the User object.</span></span> 
- <span data-ttu-id="c4320-332">"application": 클레임의 데이터가 응용 프로그램(클라이언트) 서비스 주체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-332">"application": The data in the claim is a property on the application (client) service principal.</span></span> 
- <span data-ttu-id="c4320-333">"resource": 클레임의 데이터가 리소스 서비스 주체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-333">"resource": The data in the claim is a property on the resource service principal.</span></span>
- <span data-ttu-id="c4320-334">"audience": 클레임의 데이터가 토큰의 대상 그룹인 서비스 주체(클라이언트 또는 리소스 서비스 주체)의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-334">"audience": The data in the claim is a property on the service principal that is the audience of the token (either the client or resource service principal).</span></span>
- <span data-ttu-id="c4320-335">"company": 클레임의 데이터가 리소스 테넌트에 대한 Company 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-335">“company”: The data in the claim is a property on the resource tenant’s Company object.</span></span>
- <span data-ttu-id="c4320-336">"transformation": 클레임의 데이터가 클레임 변환에서 제공됩니다(이 문서의 뒷부분에서 "클레임 변환" 섹션을 참조).</span><span class="sxs-lookup"><span data-stu-id="c4320-336">"transformation": The data in the claim is from claims transformation (see the "Claims transformation" section later in this article).</span></span> 

<span data-ttu-id="c4320-337">원본이 변환인 경우 **TransformationID** 요소도 이 클레임 정의에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-337">If the source is transformation, the **TransformationID** element must be included in this claim definition as well.</span></span>

<span data-ttu-id="c4320-338">ID 요소는 클레임의 값을 제공할 원본의 속성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-338">The ID element identifies which property on the source provides the value for the claim.</span></span> <span data-ttu-id="c4320-339">다음 표는 각 Source 값에 유효한 ID 값을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-339">The following table lists the values of ID valid for each value of Source.</span></span>

#### <a name="table-3-valid-id-values-per-source"></a><span data-ttu-id="c4320-340">표 3: 원본별 유효한 ID 값</span><span class="sxs-lookup"><span data-stu-id="c4320-340">Table 3: Valid ID values per source</span></span>
|<span data-ttu-id="c4320-341">원본</span><span class="sxs-lookup"><span data-stu-id="c4320-341">Source</span></span>|<span data-ttu-id="c4320-342">ID</span><span class="sxs-lookup"><span data-stu-id="c4320-342">ID</span></span>|<span data-ttu-id="c4320-343">설명</span><span class="sxs-lookup"><span data-stu-id="c4320-343">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="c4320-344">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-344">User</span></span>|<span data-ttu-id="c4320-345">surname</span><span class="sxs-lookup"><span data-stu-id="c4320-345">surname</span></span>|<span data-ttu-id="c4320-346">성</span><span class="sxs-lookup"><span data-stu-id="c4320-346">Family Name</span></span>|
|<span data-ttu-id="c4320-347">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-347">User</span></span>|<span data-ttu-id="c4320-348">givenname</span><span class="sxs-lookup"><span data-stu-id="c4320-348">givenname</span></span>|<span data-ttu-id="c4320-349">이름</span><span class="sxs-lookup"><span data-stu-id="c4320-349">Given Name</span></span>|
|<span data-ttu-id="c4320-350">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-350">User</span></span>|<span data-ttu-id="c4320-351">displayname</span><span class="sxs-lookup"><span data-stu-id="c4320-351">displayname</span></span>|<span data-ttu-id="c4320-352">표시 이름</span><span class="sxs-lookup"><span data-stu-id="c4320-352">Display Name</span></span>|
|<span data-ttu-id="c4320-353">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-353">User</span></span>|<span data-ttu-id="c4320-354">objectId</span><span class="sxs-lookup"><span data-stu-id="c4320-354">objectid</span></span>|<span data-ttu-id="c4320-355">ObjectID</span><span class="sxs-lookup"><span data-stu-id="c4320-355">ObjectID</span></span>|
|<span data-ttu-id="c4320-356">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-356">User</span></span>|<span data-ttu-id="c4320-357">mail</span><span class="sxs-lookup"><span data-stu-id="c4320-357">mail</span></span>|<span data-ttu-id="c4320-358">메일 주소</span><span class="sxs-lookup"><span data-stu-id="c4320-358">Email Address</span></span>|
|<span data-ttu-id="c4320-359">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-359">User</span></span>|<span data-ttu-id="c4320-360">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="c4320-360">userprincipalname</span></span>|<span data-ttu-id="c4320-361">사용자 계정 이름</span><span class="sxs-lookup"><span data-stu-id="c4320-361">User Principal Name</span></span>|
|<span data-ttu-id="c4320-362">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-362">User</span></span>|<span data-ttu-id="c4320-363">department</span><span class="sxs-lookup"><span data-stu-id="c4320-363">department</span></span>|<span data-ttu-id="c4320-364">department</span><span class="sxs-lookup"><span data-stu-id="c4320-364">Department</span></span>|
|<span data-ttu-id="c4320-365">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-365">User</span></span>|<span data-ttu-id="c4320-366">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="c4320-366">onpremisessamaccountname</span></span>|<span data-ttu-id="c4320-367">온-프레미스 SAM 계정 이름</span><span class="sxs-lookup"><span data-stu-id="c4320-367">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="c4320-368">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-368">User</span></span>|<span data-ttu-id="c4320-369">netbiosname</span><span class="sxs-lookup"><span data-stu-id="c4320-369">netbiosname</span></span>|<span data-ttu-id="c4320-370">NetBios 이름</span><span class="sxs-lookup"><span data-stu-id="c4320-370">NetBios Name</span></span>|
|<span data-ttu-id="c4320-371">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-371">User</span></span>|<span data-ttu-id="c4320-372">dnsdomainname</span><span class="sxs-lookup"><span data-stu-id="c4320-372">dnsdomainname</span></span>|<span data-ttu-id="c4320-373">DNS 도메인 이름</span><span class="sxs-lookup"><span data-stu-id="c4320-373">Dns Domain Name</span></span>|
|<span data-ttu-id="c4320-374">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-374">User</span></span>|<span data-ttu-id="c4320-375">onpremisesecurityidentifier</span><span class="sxs-lookup"><span data-stu-id="c4320-375">onpremisesecurityidentifier</span></span>|<span data-ttu-id="c4320-376">온-프레미스 보안 식별자</span><span class="sxs-lookup"><span data-stu-id="c4320-376">on-premises Security Identifier</span></span>|
|<span data-ttu-id="c4320-377">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-377">User</span></span>|<span data-ttu-id="c4320-378">companyname</span><span class="sxs-lookup"><span data-stu-id="c4320-378">companyname</span></span>|<span data-ttu-id="c4320-379">조직 이름</span><span class="sxs-lookup"><span data-stu-id="c4320-379">Organization Name</span></span>|
|<span data-ttu-id="c4320-380">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-380">User</span></span>|<span data-ttu-id="c4320-381">streetaddress</span><span class="sxs-lookup"><span data-stu-id="c4320-381">streetaddress</span></span>|<span data-ttu-id="c4320-382">주소</span><span class="sxs-lookup"><span data-stu-id="c4320-382">Street Address</span></span>|
|<span data-ttu-id="c4320-383">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-383">User</span></span>|<span data-ttu-id="c4320-384">postalcode</span><span class="sxs-lookup"><span data-stu-id="c4320-384">postalcode</span></span>|<span data-ttu-id="c4320-385">우편 번호</span><span class="sxs-lookup"><span data-stu-id="c4320-385">Postal Code</span></span>|
|<span data-ttu-id="c4320-386">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-386">User</span></span>|<span data-ttu-id="c4320-387">preferredlanguange</span><span class="sxs-lookup"><span data-stu-id="c4320-387">preferredlanguange</span></span>|<span data-ttu-id="c4320-388">기본 설정 언어</span><span class="sxs-lookup"><span data-stu-id="c4320-388">Preferred Language</span></span>|
|<span data-ttu-id="c4320-389">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-389">User</span></span>|<span data-ttu-id="c4320-390">onpremisesuserprincipalname</span><span class="sxs-lookup"><span data-stu-id="c4320-390">onpremisesuserprincipalname</span></span>|<span data-ttu-id="c4320-391">온-프레미스 UPN</span><span class="sxs-lookup"><span data-stu-id="c4320-391">on-premises UPN</span></span>|
|<span data-ttu-id="c4320-392">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-392">User</span></span>|<span data-ttu-id="c4320-393">mailNickname</span><span class="sxs-lookup"><span data-stu-id="c4320-393">mailnickname</span></span>|<span data-ttu-id="c4320-394">메일 애칭</span><span class="sxs-lookup"><span data-stu-id="c4320-394">Mail Nickname</span></span>|
|<span data-ttu-id="c4320-395">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-395">User</span></span>|<span data-ttu-id="c4320-396">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="c4320-396">extensionattribute1</span></span>|<span data-ttu-id="c4320-397">확장 특성 1</span><span class="sxs-lookup"><span data-stu-id="c4320-397">Extension Attribute 1</span></span>|
|<span data-ttu-id="c4320-398">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-398">User</span></span>|<span data-ttu-id="c4320-399">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="c4320-399">extensionattribute2</span></span>|<span data-ttu-id="c4320-400">확장 특성 2</span><span class="sxs-lookup"><span data-stu-id="c4320-400">Extension Attribute 2</span></span>|
|<span data-ttu-id="c4320-401">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-401">User</span></span>|<span data-ttu-id="c4320-402">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="c4320-402">extensionattribute3</span></span>|<span data-ttu-id="c4320-403">확장 특성 3</span><span class="sxs-lookup"><span data-stu-id="c4320-403">Extension Attribute 3</span></span>|
|<span data-ttu-id="c4320-404">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-404">User</span></span>|<span data-ttu-id="c4320-405">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="c4320-405">extensionattribute4</span></span>|<span data-ttu-id="c4320-406">확장 특성 4</span><span class="sxs-lookup"><span data-stu-id="c4320-406">Extension Attribute 4</span></span>|
|<span data-ttu-id="c4320-407">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-407">User</span></span>|<span data-ttu-id="c4320-408">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="c4320-408">extensionattribute5</span></span>|<span data-ttu-id="c4320-409">확장 특성 5</span><span class="sxs-lookup"><span data-stu-id="c4320-409">Extension Attribute 5</span></span>|
|<span data-ttu-id="c4320-410">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-410">User</span></span>|<span data-ttu-id="c4320-411">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="c4320-411">extensionattribute6</span></span>|<span data-ttu-id="c4320-412">확장 특성 6</span><span class="sxs-lookup"><span data-stu-id="c4320-412">Extension Attribute 6</span></span>|
|<span data-ttu-id="c4320-413">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-413">User</span></span>|<span data-ttu-id="c4320-414">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="c4320-414">extensionattribute7</span></span>|<span data-ttu-id="c4320-415">확장 특성 7</span><span class="sxs-lookup"><span data-stu-id="c4320-415">Extension Attribute 7</span></span>|
|<span data-ttu-id="c4320-416">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-416">User</span></span>|<span data-ttu-id="c4320-417">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="c4320-417">extensionattribute8</span></span>|<span data-ttu-id="c4320-418">확장 특성 8</span><span class="sxs-lookup"><span data-stu-id="c4320-418">Extension Attribute 8</span></span>|
|<span data-ttu-id="c4320-419">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-419">User</span></span>|<span data-ttu-id="c4320-420">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="c4320-420">extensionattribute9</span></span>|<span data-ttu-id="c4320-421">확장 특성 9</span><span class="sxs-lookup"><span data-stu-id="c4320-421">Extension Attribute 9</span></span>|
|<span data-ttu-id="c4320-422">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-422">User</span></span>|<span data-ttu-id="c4320-423">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="c4320-423">extensionattribute10</span></span>|<span data-ttu-id="c4320-424">확장 특성 10</span><span class="sxs-lookup"><span data-stu-id="c4320-424">Extension Attribute 10</span></span>|
|<span data-ttu-id="c4320-425">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-425">User</span></span>|<span data-ttu-id="c4320-426">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="c4320-426">extensionattribute11</span></span>|<span data-ttu-id="c4320-427">확장 특성 11</span><span class="sxs-lookup"><span data-stu-id="c4320-427">Extension Attribute 11</span></span>|
|<span data-ttu-id="c4320-428">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-428">User</span></span>|<span data-ttu-id="c4320-429">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="c4320-429">extensionattribute12</span></span>|<span data-ttu-id="c4320-430">확장 특성 12</span><span class="sxs-lookup"><span data-stu-id="c4320-430">Extension Attribute 12</span></span>|
|<span data-ttu-id="c4320-431">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-431">User</span></span>|<span data-ttu-id="c4320-432">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="c4320-432">extensionattribute13</span></span>|<span data-ttu-id="c4320-433">확장 특성 13</span><span class="sxs-lookup"><span data-stu-id="c4320-433">Extension Attribute 13</span></span>|
|<span data-ttu-id="c4320-434">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-434">User</span></span>|<span data-ttu-id="c4320-435">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="c4320-435">extensionattribute14</span></span>|<span data-ttu-id="c4320-436">확장 특성 14</span><span class="sxs-lookup"><span data-stu-id="c4320-436">Extension Attribute 14</span></span>|
|<span data-ttu-id="c4320-437">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-437">User</span></span>|<span data-ttu-id="c4320-438">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="c4320-438">extensionattribute15</span></span>|<span data-ttu-id="c4320-439">확장 특성 15</span><span class="sxs-lookup"><span data-stu-id="c4320-439">Extension Attribute 15</span></span>|
|<span data-ttu-id="c4320-440">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-440">User</span></span>|<span data-ttu-id="c4320-441">othermail</span><span class="sxs-lookup"><span data-stu-id="c4320-441">othermail</span></span>|<span data-ttu-id="c4320-442">다른 메일</span><span class="sxs-lookup"><span data-stu-id="c4320-442">Other Mail</span></span>|
|<span data-ttu-id="c4320-443">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-443">User</span></span>|<span data-ttu-id="c4320-444">country</span><span class="sxs-lookup"><span data-stu-id="c4320-444">country</span></span>|<span data-ttu-id="c4320-445">국가</span><span class="sxs-lookup"><span data-stu-id="c4320-445">Country</span></span>|
|<span data-ttu-id="c4320-446">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-446">User</span></span>|<span data-ttu-id="c4320-447">city</span><span class="sxs-lookup"><span data-stu-id="c4320-447">city</span></span>|<span data-ttu-id="c4320-448">City</span><span class="sxs-lookup"><span data-stu-id="c4320-448">City</span></span>|
|<span data-ttu-id="c4320-449">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-449">User</span></span>|<span data-ttu-id="c4320-450">state</span><span class="sxs-lookup"><span data-stu-id="c4320-450">state</span></span>|<span data-ttu-id="c4320-451">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="c4320-451">State</span></span>|
|<span data-ttu-id="c4320-452">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-452">User</span></span>|<span data-ttu-id="c4320-453">jobtitle</span><span class="sxs-lookup"><span data-stu-id="c4320-453">jobtitle</span></span>|<span data-ttu-id="c4320-454">직위</span><span class="sxs-lookup"><span data-stu-id="c4320-454">Job Title</span></span>|
|<span data-ttu-id="c4320-455">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-455">User</span></span>|<span data-ttu-id="c4320-456">employeeid</span><span class="sxs-lookup"><span data-stu-id="c4320-456">employeeid</span></span>|<span data-ttu-id="c4320-457">직원 ID</span><span class="sxs-lookup"><span data-stu-id="c4320-457">Employee ID</span></span>|
|<span data-ttu-id="c4320-458">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-458">User</span></span>|<span data-ttu-id="c4320-459">facsimiletelephonenumber</span><span class="sxs-lookup"><span data-stu-id="c4320-459">facsimiletelephonenumber</span></span>|<span data-ttu-id="c4320-460">팩스 번호</span><span class="sxs-lookup"><span data-stu-id="c4320-460">Facsimile Telephone Number</span></span>|
|<span data-ttu-id="c4320-461">응용 프로그램, 리소스, 대상 그룹</span><span class="sxs-lookup"><span data-stu-id="c4320-461">application, resource, audience</span></span>|<span data-ttu-id="c4320-462">displayname</span><span class="sxs-lookup"><span data-stu-id="c4320-462">displayname</span></span>|<span data-ttu-id="c4320-463">표시 이름</span><span class="sxs-lookup"><span data-stu-id="c4320-463">Display Name</span></span>|
|<span data-ttu-id="c4320-464">응용 프로그램, 리소스, 대상 그룹</span><span class="sxs-lookup"><span data-stu-id="c4320-464">application, resource, audience</span></span>|<span data-ttu-id="c4320-465">objected</span><span class="sxs-lookup"><span data-stu-id="c4320-465">objected</span></span>|<span data-ttu-id="c4320-466">ObjectID</span><span class="sxs-lookup"><span data-stu-id="c4320-466">ObjectID</span></span>|
|<span data-ttu-id="c4320-467">응용 프로그램, 리소스, 대상 그룹</span><span class="sxs-lookup"><span data-stu-id="c4320-467">application, resource, audience</span></span>|<span data-ttu-id="c4320-468">tags</span><span class="sxs-lookup"><span data-stu-id="c4320-468">tags</span></span>|<span data-ttu-id="c4320-469">서비스 주체 태그</span><span class="sxs-lookup"><span data-stu-id="c4320-469">Service Principal Tag</span></span>|
|<span data-ttu-id="c4320-470">회사</span><span class="sxs-lookup"><span data-stu-id="c4320-470">Company</span></span>|<span data-ttu-id="c4320-471">tenantcountry</span><span class="sxs-lookup"><span data-stu-id="c4320-471">tenantcountry</span></span>|<span data-ttu-id="c4320-472">테넌트 국가</span><span class="sxs-lookup"><span data-stu-id="c4320-472">Tenant’s country</span></span>|

<span data-ttu-id="c4320-473">**TransformationID:** TransformationID 요소는 Source 요소가 "변환"으로 설정된 경우에만 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-473">**TransformationID:** The TransformationID element must be provided only if the Source element is set to “transformation”.</span></span>

- <span data-ttu-id="c4320-474">이 요소는 이 클레임에 대한 데이터가 생성되는 방식을 정의하는 **ClaimsTransformation** 속성에서 변환 항목의 ID 요소와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-474">This element must match the ID element of the transformation entry in the **ClaimsTransformation** property that defines how the data for this claim is generated.</span></span>

<span data-ttu-id="c4320-475">**클레임 형식:** **JwtClaimType** 및 **SamlClaimType** 요소는 이 클레임 스키마 항목이 참조하는 클레임을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-475">**Claim Type:** The **JwtClaimType** and **SamlClaimType** elements define which claim this claim schema entry refers to.</span></span>

- <span data-ttu-id="c4320-476">JwtClaimType에는 JWT로 내보낼 클레임 이름이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-476">The JwtClaimType must contain the name of the claim to be emitted in JWTs.</span></span>
- <span data-ttu-id="c4320-477">SamlClaimType에는 SAML 토큰으로 내보낼 클레임 URI가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-477">The SamlClaimType must contain the URI of the claim to be emitted in SAML tokens.</span></span>

>[!NOTE]
><span data-ttu-id="c4320-478">제한된 클레임 집합에 있는 클레임의 이름 및 URI는 클레임 형식 요소에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-478">Names and URIs of claims in the restricted claim set cannot be used for the claim type elements.</span></span> <span data-ttu-id="c4320-479">자세한 내용은 이 문서의 뒷부분에 나오는 "예외 및 제한 사항" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4320-479">For more information, see the "Exceptions and restrictions" section later in this article.</span></span>

### <a name="claims-transformation"></a><span data-ttu-id="c4320-480">클레임 변환</span><span class="sxs-lookup"><span data-stu-id="c4320-480">Claims transformation</span></span>

<span data-ttu-id="c4320-481">**문자열:** ClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="c4320-481">**String:** ClaimsTransformation</span></span>

<span data-ttu-id="c4320-482">**데이터 형식:** 하나 이상의 변환 항목을 가진 JSON Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-482">**Data type:** JSON blob, with one or more transformation entries</span></span> 

<span data-ttu-id="c4320-483">**요약:** 이 속성을 사용하여 클레임 스키마에 지정된 클레임에 대한 출력 데이터를 생성하기 위해 원본 데이터에 일반 변환을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-483">**Summary:** Use this property to apply common transformations to source data, to generate the output data for claims specified in the Claims Schema.</span></span>

<span data-ttu-id="c4320-484">**ID:** ID 요소를 사용하여 클레임 스키마 항목의 TransformationID에서 이 변환 항목을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-484">**ID:** Use the ID element to reference this transformation entry in the TransformationID Claims Schema entry.</span></span> <span data-ttu-id="c4320-485">이 값은 이 정책 내에서 각 변환 항목에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-485">This value must be unique for each transformation entry within this policy.</span></span>

<span data-ttu-id="c4320-486">**TransformationMethod:** TransformationMethod 요소는 클레임에 대한 데이터를 생성하기 위해 수행할 작업을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-486">**TransformationMethod:** The TransformationMethod element identifies which operation is performed to generate the data for the claim.</span></span>

<span data-ttu-id="c4320-487">선택한 방법에 따라 입력 및 출력 집합이 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-487">Based on the method chosen, a set of inputs and outputs is expected.</span></span> <span data-ttu-id="c4320-488">이러한 값은 **InputClaims**, **InputParameters** 및 **OutputClaims** 요소를 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-488">These are defined by using the **InputClaims**, **InputParameters** and **OutputClaims** elements.</span></span>

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a><span data-ttu-id="c4320-489">표 4: 변환 메서드 및 예상 입력 및 출력</span><span class="sxs-lookup"><span data-stu-id="c4320-489">Table 4: Transformation methods and expected inputs and outputs</span></span>
|<span data-ttu-id="c4320-490">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="c4320-490">TransformationMethod</span></span>|<span data-ttu-id="c4320-491">예상 입력</span><span class="sxs-lookup"><span data-stu-id="c4320-491">Expected input</span></span>|<span data-ttu-id="c4320-492">예상 출력</span><span class="sxs-lookup"><span data-stu-id="c4320-492">Expected output</span></span>|<span data-ttu-id="c4320-493">설명</span><span class="sxs-lookup"><span data-stu-id="c4320-493">Description</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="c4320-494">Join</span><span class="sxs-lookup"><span data-stu-id="c4320-494">Join</span></span>|<span data-ttu-id="c4320-495">string1, string2, 구분 기호</span><span class="sxs-lookup"><span data-stu-id="c4320-495">string1, string2, separator</span></span>|<span data-ttu-id="c4320-496">outputClaim</span><span class="sxs-lookup"><span data-stu-id="c4320-496">outputClaim</span></span>|<span data-ttu-id="c4320-497">구분 기호를 사용하여 입력 문자열을 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-497">Joins input strings by using a separator in between.</span></span> <span data-ttu-id="c4320-498">예: string1:"foo@bar.com" , string2:"sandbox" , separator:"."는 outputClaim:"foo@bar.com.sandbox"를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-498">For example: string1:"foo@bar.com" , string2:"sandbox" , separator:"." results in outputClaim:"foo@bar.com.sandbox"</span></span>|
|<span data-ttu-id="c4320-499">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="c4320-499">ExtractMailPrefix</span></span>|<span data-ttu-id="c4320-500">mail</span><span class="sxs-lookup"><span data-stu-id="c4320-500">mail</span></span>|<span data-ttu-id="c4320-501">outputClaim</span><span class="sxs-lookup"><span data-stu-id="c4320-501">outputClaim</span></span>|<span data-ttu-id="c4320-502">메일 주소의 로컬 부분을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-502">Extracts the local part of an email address.</span></span> <span data-ttu-id="c4320-503">예: mail:"foo@bar.com"은 outputClaim:"foo"를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-503">For example: mail:"foo@bar.com" results in outputClaim:"foo".</span></span> <span data-ttu-id="c4320-504">@ 기호가 없으면 원본 입력 문자열이 현재 그대로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-504">If no @ sign is present, then the orignal input string is returned as is.</span></span>|

<span data-ttu-id="c4320-505">**InputClaims:** InputClaims 요소를 사용하여 클레임 스키마 항목에서 변환에 데이터를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-505">**InputClaims:** Use an InputClaims element to pass the data from a claim schema entry to a transformation.</span></span> <span data-ttu-id="c4320-506">두 개의 특성인 **ClaimTypeReferenceId** 및 **TransformationClaimType**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-506">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="c4320-507">**ClaimTypeReferenceId**가 클레임 스키마 항목의 ID 요소와 조인되어 적절한 입력 클레임을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-507">**ClaimTypeReferenceId** is joined with ID element of the claim schema entry to find the appropriate input claim.</span></span> 
- <span data-ttu-id="c4320-508">**TransformationClaimType**은 이 입력에 고유 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-508">**TransformationClaimType** is used to give a unique name to this input.</span></span> <span data-ttu-id="c4320-509">이 이름은 변환 방법에 대한 예상 입력 중 하나와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-509">This name must match one of the expected inputs for the transformation method.</span></span>

<span data-ttu-id="c4320-510">**InputParameters:** InputParameters 요소를 사용하여 변환에 상수 값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-510">**InputParameters:** Use an InputParameters element to pass a constant value to a transformation.</span></span> <span data-ttu-id="c4320-511">두 개의 특성인 **Value** 및 **ID**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-511">It has two attributes: **Value** and **ID**.</span></span>

- <span data-ttu-id="c4320-512">**Value**는 전달할 실제 상수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-512">**Value** is the actual constant value to be passed.</span></span>
- <span data-ttu-id="c4320-513">**ID**는 이 입력에 고유 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-513">**ID** is used to give a unique name to this input.</span></span> <span data-ttu-id="c4320-514">이 이름은 변환 방법에 대한 예상 입력 중 하나와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-514">This name must match one of the expected inputs for the transformation method.</span></span>

<span data-ttu-id="c4320-515">**OutputClaims:** OutputClaims 요소를 사용하여 변환에 의해 생성된 데이터를 보관하고 클레임 스키마 항목에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-515">**OutputClaims:** Use an OutputClaims element to hold the data generated by a transformation, and tie it to a claim schema entry.</span></span> <span data-ttu-id="c4320-516">두 개의 특성인 **ClaimTypeReferenceId** 및 **TransformationClaimType**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-516">It has two attributes: **ClaimTypeReferenceId** and **TransformationClaimType**.</span></span>

- <span data-ttu-id="c4320-517">**ClaimTypeReferenceId**가 클레임 스키마 항목의 ID와 조인되어 적절한 출력 클레임을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-517">**ClaimTypeReferenceId** is joined with the ID of the claim schema entry to find the appropriate output claim.</span></span>
- <span data-ttu-id="c4320-518">**TransformationClaimType**은 이 출력에 고유 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-518">**TransformationClaimType** is used to give a unique name to this output.</span></span> <span data-ttu-id="c4320-519">이 이름은 변환 방법에 대한 예상 출력 중 하나와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-519">This name must match one of the expected outputs for the transformation method.</span></span>

### <a name="exceptions-and-restrictions"></a><span data-ttu-id="c4320-520">예외 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="c4320-520">Exceptions and restrictions</span></span>

<span data-ttu-id="c4320-521">**SAML NameID 및 UPN:** NameID 및 UPN 값을 소싱하는 특성과 허용되는 클레임 변환은 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-521">**SAML NameID and UPN:** The attributes from which you source the NameID and UPN values, and the claims transformations that are permitted, are limited.</span></span>

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a><span data-ttu-id="c4320-522">표 5: SAML NameID에 대한 데이터 원본으로 허용되는 특성</span><span class="sxs-lookup"><span data-stu-id="c4320-522">Table 5: Attributes allowed as a data source for SAML NameID</span></span>
|<span data-ttu-id="c4320-523">원본</span><span class="sxs-lookup"><span data-stu-id="c4320-523">Source</span></span>|<span data-ttu-id="c4320-524">ID</span><span class="sxs-lookup"><span data-stu-id="c4320-524">ID</span></span>|<span data-ttu-id="c4320-525">설명</span><span class="sxs-lookup"><span data-stu-id="c4320-525">Description</span></span>|
|-----|-----|-----|
|<span data-ttu-id="c4320-526">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-526">User</span></span>|<span data-ttu-id="c4320-527">mail</span><span class="sxs-lookup"><span data-stu-id="c4320-527">mail</span></span>|<span data-ttu-id="c4320-528">메일 주소</span><span class="sxs-lookup"><span data-stu-id="c4320-528">Email Address</span></span>|
|<span data-ttu-id="c4320-529">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-529">User</span></span>|<span data-ttu-id="c4320-530">userprincipalname</span><span class="sxs-lookup"><span data-stu-id="c4320-530">userprincipalname</span></span>|<span data-ttu-id="c4320-531">사용자 계정 이름</span><span class="sxs-lookup"><span data-stu-id="c4320-531">User Principal Name</span></span>|
|<span data-ttu-id="c4320-532">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-532">User</span></span>|<span data-ttu-id="c4320-533">onpremisessamaccountname</span><span class="sxs-lookup"><span data-stu-id="c4320-533">onpremisessamaccountname</span></span>|<span data-ttu-id="c4320-534">온-프레미스 SAM 계정 이름</span><span class="sxs-lookup"><span data-stu-id="c4320-534">On Premises Sam Account Name</span></span>|
|<span data-ttu-id="c4320-535">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-535">User</span></span>|<span data-ttu-id="c4320-536">employeeid</span><span class="sxs-lookup"><span data-stu-id="c4320-536">employeeid</span></span>|<span data-ttu-id="c4320-537">직원 ID</span><span class="sxs-lookup"><span data-stu-id="c4320-537">Employee ID</span></span>|
|<span data-ttu-id="c4320-538">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-538">User</span></span>|<span data-ttu-id="c4320-539">extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="c4320-539">extensionattribute1</span></span>|<span data-ttu-id="c4320-540">확장 특성 1</span><span class="sxs-lookup"><span data-stu-id="c4320-540">Extension Attribute 1</span></span>|
|<span data-ttu-id="c4320-541">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-541">User</span></span>|<span data-ttu-id="c4320-542">extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="c4320-542">extensionattribute2</span></span>|<span data-ttu-id="c4320-543">확장 특성 2</span><span class="sxs-lookup"><span data-stu-id="c4320-543">Extension Attribute 2</span></span>|
|<span data-ttu-id="c4320-544">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-544">User</span></span>|<span data-ttu-id="c4320-545">extensionattribute3</span><span class="sxs-lookup"><span data-stu-id="c4320-545">extensionattribute3</span></span>|<span data-ttu-id="c4320-546">확장 특성 3</span><span class="sxs-lookup"><span data-stu-id="c4320-546">Extension Attribute 3</span></span>|
|<span data-ttu-id="c4320-547">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-547">User</span></span>|<span data-ttu-id="c4320-548">extensionattribute4</span><span class="sxs-lookup"><span data-stu-id="c4320-548">extensionattribute4</span></span>|<span data-ttu-id="c4320-549">확장 특성 4</span><span class="sxs-lookup"><span data-stu-id="c4320-549">Extension Attribute 4</span></span>|
|<span data-ttu-id="c4320-550">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-550">User</span></span>|<span data-ttu-id="c4320-551">extensionattribute5</span><span class="sxs-lookup"><span data-stu-id="c4320-551">extensionattribute5</span></span>|<span data-ttu-id="c4320-552">확장 특성 5</span><span class="sxs-lookup"><span data-stu-id="c4320-552">Extension Attribute 5</span></span>|
|<span data-ttu-id="c4320-553">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-553">User</span></span>|<span data-ttu-id="c4320-554">extensionattribute6</span><span class="sxs-lookup"><span data-stu-id="c4320-554">extensionattribute6</span></span>|<span data-ttu-id="c4320-555">확장 특성 6</span><span class="sxs-lookup"><span data-stu-id="c4320-555">Extension Attribute 6</span></span>|
|<span data-ttu-id="c4320-556">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-556">User</span></span>|<span data-ttu-id="c4320-557">extensionattribute7</span><span class="sxs-lookup"><span data-stu-id="c4320-557">extensionattribute7</span></span>|<span data-ttu-id="c4320-558">확장 특성 7</span><span class="sxs-lookup"><span data-stu-id="c4320-558">Extension Attribute 7</span></span>|
|<span data-ttu-id="c4320-559">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-559">User</span></span>|<span data-ttu-id="c4320-560">extensionattribute8</span><span class="sxs-lookup"><span data-stu-id="c4320-560">extensionattribute8</span></span>|<span data-ttu-id="c4320-561">확장 특성 8</span><span class="sxs-lookup"><span data-stu-id="c4320-561">Extension Attribute 8</span></span>|
|<span data-ttu-id="c4320-562">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-562">User</span></span>|<span data-ttu-id="c4320-563">extensionattribute9</span><span class="sxs-lookup"><span data-stu-id="c4320-563">extensionattribute9</span></span>|<span data-ttu-id="c4320-564">확장 특성 9</span><span class="sxs-lookup"><span data-stu-id="c4320-564">Extension Attribute 9</span></span>|
|<span data-ttu-id="c4320-565">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-565">User</span></span>|<span data-ttu-id="c4320-566">extensionattribute10</span><span class="sxs-lookup"><span data-stu-id="c4320-566">extensionattribute10</span></span>|<span data-ttu-id="c4320-567">확장 특성 10</span><span class="sxs-lookup"><span data-stu-id="c4320-567">Extension Attribute 10</span></span>|
|<span data-ttu-id="c4320-568">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-568">User</span></span>|<span data-ttu-id="c4320-569">extensionattribute11</span><span class="sxs-lookup"><span data-stu-id="c4320-569">extensionattribute11</span></span>|<span data-ttu-id="c4320-570">확장 특성 11</span><span class="sxs-lookup"><span data-stu-id="c4320-570">Extension Attribute 11</span></span>|
|<span data-ttu-id="c4320-571">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-571">User</span></span>|<span data-ttu-id="c4320-572">extensionattribute12</span><span class="sxs-lookup"><span data-stu-id="c4320-572">extensionattribute12</span></span>|<span data-ttu-id="c4320-573">확장 특성 12</span><span class="sxs-lookup"><span data-stu-id="c4320-573">Extension Attribute 12</span></span>|
|<span data-ttu-id="c4320-574">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-574">User</span></span>|<span data-ttu-id="c4320-575">extensionattribute13</span><span class="sxs-lookup"><span data-stu-id="c4320-575">extensionattribute13</span></span>|<span data-ttu-id="c4320-576">확장 특성 13</span><span class="sxs-lookup"><span data-stu-id="c4320-576">Extension Attribute 13</span></span>|
|<span data-ttu-id="c4320-577">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-577">User</span></span>|<span data-ttu-id="c4320-578">extensionattribute14</span><span class="sxs-lookup"><span data-stu-id="c4320-578">extensionattribute14</span></span>|<span data-ttu-id="c4320-579">확장 특성 14</span><span class="sxs-lookup"><span data-stu-id="c4320-579">Extension Attribute 14</span></span>|
|<span data-ttu-id="c4320-580">사용자</span><span class="sxs-lookup"><span data-stu-id="c4320-580">User</span></span>|<span data-ttu-id="c4320-581">extensionattribute15</span><span class="sxs-lookup"><span data-stu-id="c4320-581">extensionattribute15</span></span>|<span data-ttu-id="c4320-582">확장 특성 15</span><span class="sxs-lookup"><span data-stu-id="c4320-582">Extension Attribute 15</span></span>|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a><span data-ttu-id="c4320-583">표 6: SAML NameID에 허용되는 변환 메서드</span><span class="sxs-lookup"><span data-stu-id="c4320-583">Table 6: Transformation methods allowed for SAML NameID</span></span>
|<span data-ttu-id="c4320-584">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="c4320-584">TransformationMethod</span></span>|<span data-ttu-id="c4320-585">제한</span><span class="sxs-lookup"><span data-stu-id="c4320-585">Restrictions</span></span>|
| ----- | ----- |
|<span data-ttu-id="c4320-586">ExtractMailPrefix</span><span class="sxs-lookup"><span data-stu-id="c4320-586">ExtractMailPrefix</span></span>|<span data-ttu-id="c4320-587">없음</span><span class="sxs-lookup"><span data-stu-id="c4320-587">None</span></span>|
|<span data-ttu-id="c4320-588">Join</span><span class="sxs-lookup"><span data-stu-id="c4320-588">Join</span></span>|<span data-ttu-id="c4320-589">조인되는 접미사는 리소스 테넌트의 확인된 도메인이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-589">The suffix being joined must be a verified domain of the resource tenant.</span></span>|

### <a name="custom-signing-key"></a><span data-ttu-id="c4320-590">사용자 지정 서명 키</span><span class="sxs-lookup"><span data-stu-id="c4320-590">Custom signing key</span></span>
<span data-ttu-id="c4320-591">클레임 매핑 정책을 적용하려면 사용자 지정 서명 키를 서비스 사용자 개체에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-591">A custom signing key must be assigned to the service principal object for a claims mapping policy to take effect.</span></span> <span data-ttu-id="c4320-592">정책의 영향을 받은 발급된 모든 토큰이 이 키로 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-592">All tokens issued that have been impacted by the policy are signed with this key.</span></span> <span data-ttu-id="c4320-593">이 키로 서명된 토큰을 수락하도록 응용 프로그램을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-593">Applications must be configured to accept tokens signed with this key.</span></span> <span data-ttu-id="c4320-594">이렇게 하면 클레임 매핑 정책의 생성자가 토큰을 수정한 것을 인정하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-594">This ensures acknowledgment that tokens have been modified by the creator of the claims mapping policy.</span></span> <span data-ttu-id="c4320-595">이는 악의적인 행위자가 만든 클레임 매핑 정책으로부터 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-595">This protects applications from claims mapping policies created by malicious actors.</span></span>

### <a name="cross-tenant-scenarios"></a><span data-ttu-id="c4320-596">교차 테넌트 시나리오</span><span class="sxs-lookup"><span data-stu-id="c4320-596">Cross-tenant scenarios</span></span>
<span data-ttu-id="c4320-597">클레임 매핑 정책이 게스트 사용자에게 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-597">Claims mapping policies do not apply to guest users.</span></span> <span data-ttu-id="c4320-598">게스트 사용자가 해당 서비스 주체에 클레임 매핑 정책이 적용된 응용 프로그램에 액세스하려고 하면 기본 토큰이 발급됩니다(정책이 적용되지 않음).</span><span class="sxs-lookup"><span data-stu-id="c4320-598">If a guest user attempts to access an application with a claims mapping policy assigned to its service principal, the default token is issued (the policy has no effect).</span></span>

## <a name="claims-mapping-policy-assignment"></a><span data-ttu-id="c4320-599">클레임 매핑 정책 할당</span><span class="sxs-lookup"><span data-stu-id="c4320-599">Claims mapping policy assignment</span></span>
<span data-ttu-id="c4320-600">클레임 매핑 정책은 서비스 사용자 개체에만 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-600">Claims mapping policies can only be assigned to service principal objects.</span></span>

### <a name="example-claims-mapping-policies"></a><span data-ttu-id="c4320-601">예제 클레임 매핑 정책</span><span class="sxs-lookup"><span data-stu-id="c4320-601">Example claims mapping policies</span></span>

<span data-ttu-id="c4320-602">Azure AD에서 특정 서비스 주체에 대해 토큰에 내보내지는 클레임을 사용자 지정할 수 있는 경우 많은 시나리오가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-602">In Azure AD, many scenarios are possible when you can customize claims emitted in tokens for specific service principals.</span></span> <span data-ttu-id="c4320-603">이 섹션에서는 클레임 매핑 정책 형식을 사용하는 방법을 이해하는 데 도움이 되는 몇 가지 일반적인 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-603">In this section, we walk through a few common scenarios that can help you grasp how to use the claims mapping policy type.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="c4320-604">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c4320-604">Prerequisites</span></span>
<span data-ttu-id="c4320-605">다음 예제에서는 서비스 주체에 대한 정책을 만들고, 업데이트, 연결 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-605">In the following examples, you create, update, link, and delete policies for service principals.</span></span> <span data-ttu-id="c4320-606">Azure AD을 처음 접하는 분들은 Azure AD 테넌트를 가져오는 방법을 살펴본 후 예제를 진행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-606">If you are new to Azure AD, we recommend that you learn about how to get an Azure AD tenant before you proceed with these examples.</span></span> 

<span data-ttu-id="c4320-607">시작하려면 다음 단계 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-607">To get started, do the following steps:</span></span>


1. <span data-ttu-id="c4320-608">최신 [Azure AD PowerShell 모듈 공개 미리 보기 릴리스](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-608">Download the latest [Azure AD PowerShell Module public preview release](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).</span></span>
2.  <span data-ttu-id="c4320-609">Connect 명령을 실행하여 Azure AD 관리자 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-609">Run the Connect command to sign in to your Azure AD admin account.</span></span> <span data-ttu-id="c4320-610">새 세션을 시작할 때마다 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-610">Run this command each time you start a new session.</span></span>
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  <span data-ttu-id="c4320-611">조직에서 만든 모든 정책을 확인하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-611">To see all policies that have been created in your organization, run the following command.</span></span> <span data-ttu-id="c4320-612">다음 시나리오에서 대부분의 작업 후에 이 명령을 실행하여 정책이 예상대로 생성되는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-612">We recommend that you run this command after most operations in the following scenarios, to check that your policies are being created as expected.</span></span>
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-to-omit-the-basic-claims-from-tokens-issued-to-a-service-principal"></a><span data-ttu-id="c4320-613">예제: 서비스 주체에 발급된 토큰에서 기본 클레임을 생략하는 정책을 만들고 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-613">Example: Create and assign a policy to omit the basic claims from tokens issued to a service principal.</span></span>
<span data-ttu-id="c4320-614">이 예제에서는 연결된 서비스 주체에 발급된 토큰에서 기본 클레임 집합을 제거하는 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-614">In this example, you create a policy that removes the basic claim set from tokens issued to linked service principals.</span></span>


1. <span data-ttu-id="c4320-615">클레임 매핑 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-615">Create a claims mapping policy.</span></span> <span data-ttu-id="c4320-616">특정 서비스 주체에 연결되는 이 정책은 토큰에서 기본 클레임 집합을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-616">This policy, linked to specific service principals, removes the basic claim set from tokens.</span></span>
    1. <span data-ttu-id="c4320-617">정책을 만들려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-617">To create the policy, run this command:</span></span> 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. <span data-ttu-id="c4320-618">새 정책을 보고 정책 ObjectId를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-618">To see your new policy, and to get the policy ObjectId, run the following command:</span></span>
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="c4320-619">서비스 주체에게 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-619">Assign the policy to your service principal.</span></span> <span data-ttu-id="c4320-620">서비스 주체의 ObjectId도 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-620">You also need to get the ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="c4320-621">조직의 모든 서비스 주체를 보려면 Microsoft Graph를 쿼리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-621">To see all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="c4320-622">또는 Azure AD Graph Explorer에서 Azure AD 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-622">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span></span>
    2.  <span data-ttu-id="c4320-623">서비스 주체의 ObjectId가 있으면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-623">When you have the ObjectId of your service principal, run the following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
#### <a name="example-create-and-assign-a-policy-to-include-the-employeeid-and-tenantcountry-as-claims-in-tokens-issued-to-a-service-principal"></a><span data-ttu-id="c4320-624">예제: 서비스 주체에 발급된 토큰에서 EmployeeID 및 TenantCountry를 클레임으로 포함하는 정책을 만들고 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-624">Example: Create and assign a policy to include the EmployeeID and TenantCountry as claims in tokens issued to a service principal.</span></span>
<span data-ttu-id="c4320-625">이 예제에서는 연결된 서비스 주체에 발급된 토큰에 EmployeeID 및 TenantCountry를 추가하는 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-625">In this example, you create a policy that adds the EmployeeID and TenantCountry to tokens issued to linked service principals.</span></span> <span data-ttu-id="c4320-626">EmployeeID는 SAML 토큰 및 JWT 둘 다에서 이름 클레임 형식으로 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-626">The EmployeeID is emitted as the name claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="c4320-627">TenantCountry는 SAML 토큰 및 JWT 둘 다에서 국가 클레임 형식으로 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-627">The TenantCountry is emitted as the country claim type in both SAML tokens and JWTs.</span></span> <span data-ttu-id="c4320-628">이 예제에서는 토큰에 기본 클레임 집합을 계속 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-628">In this example, we continue to include the basic claims set in the tokens.</span></span>

1. <span data-ttu-id="c4320-629">클레임 매핑 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-629">Create a claims mapping policy.</span></span> <span data-ttu-id="c4320-630">특정 서비스 주체에 연결되는 이 정책은 토큰에 EmployeeID 및 TenantCountry 클레임을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-630">This policy, linked to specific service principals, adds the EmployeeID and TenantCountry claims to tokens.</span></span>
    1. <span data-ttu-id="c4320-631">정책을 만들려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-631">To create the policy, run this command:</span></span>  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. <span data-ttu-id="c4320-632">새 정책을 보고 정책 ObjectId를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-632">To see your new policy, and to get the policy ObjectId, run the following command:</span></span>
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="c4320-633">서비스 주체에게 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-633">Assign the policy to your service principal.</span></span> <span data-ttu-id="c4320-634">서비스 주체의 ObjectId도 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-634">You also need to get the ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="c4320-635">조직의 모든 서비스 주체를 보려면 Microsoft Graph를 쿼리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-635">To see all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="c4320-636">또는 Azure AD Graph Explorer에서 Azure AD 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-636">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span></span>
    2.  <span data-ttu-id="c4320-637">서비스 주체의 ObjectId가 있으면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-637">When you have the ObjectId of your service principal, run the following command:</span></span>  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-to-a-service-principal"></a><span data-ttu-id="c4320-638">예제: 서비스 주체에 발급된 토큰에서 클레임 변환을 이용하는 정책을 만들고 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-638">Example: Create and assign a policy that uses a claims transformation in tokens issued to a service principal.</span></span>
<span data-ttu-id="c4320-639">이 예제에서는 연결된 서비스 주체에 발급된 JWT에 사용자 지정 클레임 “JoinedData”를 내보내는 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-639">In this example, you create a policy that emits a custom claim “JoinedData” to JWTs issued to linked service principals.</span></span> <span data-ttu-id="c4320-640">이 클레임에는 사용자 개체의 extensionattribute1 특성에 저장된 데이터와 ".sandbox"를 조인하여 만든 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-640">This claim contains a value created by joining the data stored in the extensionattribute1 attribute on the user object with “.sandbox”.</span></span> <span data-ttu-id="c4320-641">이 예제에서는 토큰에 기본 클레임 집합을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-641">In this example, we exclude the basic claims set in the tokens.</span></span>


1. <span data-ttu-id="c4320-642">클레임 매핑 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-642">Create a claims mapping policy.</span></span> <span data-ttu-id="c4320-643">특정 서비스 주체에 연결되는 이 정책은 토큰에 EmployeeID 및 TenantCountry 클레임을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-643">This policy, linked to specific service principals, adds the EmployeeID and TenantCountry claims to tokens.</span></span>
    1. <span data-ttu-id="c4320-644">정책을 만들려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-644">To create the policy, run this command:</span></span> 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. <span data-ttu-id="c4320-645">새 정책을 보고 정책 ObjectId를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-645">To see your new policy, and to get the policy ObjectId, run the following command:</span></span> 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  <span data-ttu-id="c4320-646">서비스 주체에게 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-646">Assign the policy to your service principal.</span></span> <span data-ttu-id="c4320-647">서비스 주체의 ObjectId도 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-647">You also need to get the ObjectId of your service principal.</span></span> 
    1.  <span data-ttu-id="c4320-648">조직의 모든 서비스 주체를 보려면 Microsoft Graph를 쿼리하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-648">To see all your organization's service principals, you can query Microsoft Graph.</span></span> <span data-ttu-id="c4320-649">또는 Azure AD Graph Explorer에서 Azure AD 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-649">Or, in Azure AD Graph Explorer, sign in to your Azure AD account.</span></span>
    2.  <span data-ttu-id="c4320-650">서비스 주체의 ObjectId가 있으면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c4320-650">When you have the ObjectId of your service principal, run the following command:</span></span> 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
    ```
