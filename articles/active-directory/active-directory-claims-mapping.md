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
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Azure Active Directory의 클레임 매핑(공개 미리 보기)

>[!NOTE]
>이 기능은 대체 하 고 hello 대체 [사용자 지정 클레임](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) 현재 hello 포털을 통해 제공 합니다. Hello 포털을 사용 하 여 클레임을 사용자 지정 하는 경우 또한 toohello 그래프/PowerShell 메서드이 문서에에서 자세히 설명이 hello에 동일한 응용 프로그램, 해당 응용 프로그램에서 무시 hello 포털에서 hello 구성 용으로 발급 된 토큰입니다.
이 문서에에서 자세히 설명 하는 hello 메서드를 통해 구성이 hello 포털에 반영 되지 않습니다.

이 기능은 테 넌 트에 특정 응용 프로그램에 대 한 토큰에 포함 된 테 넌 트 관리자 toocustomize hello 클레임으로 사용 됩니다. 다음과 같은 경우 클레임 매핑 정책을 사용할 수 있습니다.

- 토큰에 포함할 클레임을 선택합니다.
- 아직 존재하지 않는 클레임 형식을 만듭니다.
- 선택 하거나 특정 클레임에 포함 된 데이터의 hello 원본을 변경 합니다.

>[!NOTE]
>이 기능은 현재 공개 미리 보기로 제공되고 있습니다. Toorevert 준비 하거나 변경 내용을 모두 제거 합니다. hello 기능은 공개 미리 보기 기간 동안 모든 Azure Active Directory (Azure AD) 구독에서 사용할 수 있습니다. 그러나 hello 기능이 일반 공급 되 면 hello 기능의 일부 측면 Azure Active Directory premium 구독에 필요할 수 있습니다.

## <a name="claims-mapping-policy-type"></a>클레임 매핑 정책 유형
Azure AD에서 **정책** 개체는 조직에 있는 개별 응용 프로그램 또는 모든 응용 프로그램에 적용되는 규칙 집합을 나타냅니다. 각 정책 종류가 되는 속성 집합이 있는 고유한 구조는 다음 tooobjects toowhich 할당을 적용 합니다.

A 클레임의 형식인 정책 매핑 **정책** hello를 수정 하는 개체는 특정 응용 프로그램에 발급 한 토큰에 포함 된 클레임입니다.

## <a name="claim-sets"></a>클레임 집합
토큰에 사용되는 시기와 방법을 정의하는 특정 클레임 집합이 있습니다.

### <a name="core-claim-set"></a>핵심 클레임 집합
Hello 코어에서 클레임 정책에 관계 없이 모든 토큰에 있는 집합을 요청 하십시오. 또한 이러한 클레임은 제한된 것으로 간주되며 수정할 수 없습니다.

### <a name="basic-claim-set"></a>기본 클레임 집합
hello 기본 클레임 집합에는 토큰 (더하기 toohello 코어 클레임 집합)에 대 한 기본적으로 발생 하는 hello 클레임 포함 됩니다. 이러한 클레임을 생략 하면 또는 정책 매핑 hello 클레임을 사용 하 여 수정할 수 있습니다.

### <a name="restricted-claim-set"></a>제한된 클레임 집합
정책을 사용하여 제한된 클레임을 수정할 수 없습니다. hello 데이터 소스를 변경할 수 없으며, 및 이러한 클레임을 생성 하는 경우 변환이 적용 됩니다.

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>표 1: JWT(JSON Web Token) 제한된 클레임 집합
|클레임 형식(이름)|
| ----- |
|_claim_names|
|_claim_sources|
|access_token|
|account_type|
|acr|
|actor|
|actortoken|
|aio|
|altsecid|
|amr|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|appId|
|appidacr|
|어설션|
|at_hash|
|aud|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|cc|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|cnf|
|코드|
|controls|
|credential_keys|
|csr|
|csr_type|
|deviceId|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|email|
|endpoint|
|enfpolids|
|exp|
|expires_on|
|grant_type|
|graph|
|group_sids|
|groups|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier|
|iat|
|identityprovider|
|idp|
|in_corp|
|instance|
|ipaddr|
|isbrowserhostedapp|
|iss|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|nameid|
|nbf|
|netbios_name|
|nonce|
|oid|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|password|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|puid|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|resource|
|role|
|roles|
|scope|
|scp|
|sid|
|signature|
|signin_state|
|src1|
|src2|
|sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|tid|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|upn|
|user_setting_sync_url|
|username|
|uti|
|ver|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>표 2: SAML(Security Assertion Markup Language) 제한된 클레임 집합
|클레임 형식(URI)|
| ----- |
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.microsoft.com/identity/claims/accesstoken|
|http://schemas.microsoft.com/identity/claims/openid2_id|
|http://schemas.microsoft.com/identity/claims/identityprovider|
|http://schemas.microsoft.com/identity/claims/objectidentifier|
|http://schemas.microsoft.com/identity/claims/puid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
|http://schemas.microsoft.com/identity/claims/tenantid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groups|
|http://schemas.microsoft.com/claims/groups.link|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/role|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier|
|http://schemas.microsoft.com/identity/claims/scope|

## <a name="claims-mapping-policy-properties"></a>클레임 매핑 정책 속성
클레임을 내보낸 정책 toocontrol 매핑 클레임의 hello 속성을 사용 하 고 hello 데이터에서 소싱 된 위치입니다. 설정 된 정책이 hello 시스템 hello 코어 클레임 집합을 포함 하는 토큰을 발급, hello 기본 클레임 집합을 및 응용 프로그램 hello 하는 선택적 클레임 tooreceive 선택 했습니다.

### <a name="include-basic-claim-set"></a>기본 클레임 집합 포함

**문자열:** IncludeBasicClaimSet

**데이터 형식:** 부울(True 또는 False)

**요약:** 이 속성은이 정책에 의해 영향을 받는 토큰에 hello 기본 클레임 집합에 포함 되는지 여부를 결정 합니다. 

- 경우 hello 정책에 의해 영향을 받은 토큰의 집합 tooTrue, hello 기본 클레임 집합의 모든 클레임을 내보냅니다. 
- 집합 tooFalse, hello 기본 클레임 집합의 클레임에에서 없는 경우 hello 토큰은 개별적으로 추가 hello의 hello 클레임 스키마 속성에 동일한 정책.

>[!NOTE] 
>Hello 코어의 클레임 집합은이 속성은로 설정 하는 것에 관계 없이 모든 토큰에 클레임입니다. 

### <a name="claims-schema"></a>클레임 스키마

**문자열:** ClaimsSchema

**데이터 형식:** 하나 이상의 클레임 스키마 항목을 가진 JSON Blob입니다.

**요약:** 이 속성은 hello 정책에 의해 영향을 받는 hello 토큰에 표시 되는 클레임을 정의 또한 toohello 기본 클레임 집합 및 hello 코어 클레임 집합입니다.
이 속성에 정의된 각 클레임 스키마 항목의 경우 특정 정보가 필요합니다. Hello 데이터에서 온 것인지를 지정 해야 합니다 (**값** 또는 **소스/i D 쌍**)로 내보내는 hello 데이터 클레임 및 (**클레임 유형**).

### <a name="claim-schema-entry-elements"></a>클레임 스키마 항목 요소

**값:** hello Value 요소 hello 클레임에 포함 된 hello 데이터 toobe로 정적 값을 정의 합니다.

**소스/i D 쌍:** 소스 hello 및에서 hello hello 클레임에는 데이터 원본으로 ID 요소를 정의 합니다. 

hello 소스 요소는 hello 다음의 tooone를 설정 해야 합니다. 


- "user": hello 데이터 hello에 클레임은 hello 사용자 개체에 대 한 속성이 있습니다. 
- "application": hello 데이터 hello에 클레임은 hello (클라이언트) 응용 프로그램 서비스 사용자에 대 한 속성이 있습니다. 
- "resource": hello 데이터 hello에 클레임은 hello 리소스 서비스 사용자에 대 한 속성이 있습니다.
- "audience": hello 클레임의 hello 데이터는 대상인 hello hello 토큰 (두 hello 클라이언트 또는 리소스 서비스 사용자)의 hello 서비스 사용자에 대 한 속성이 있습니다.
- "company": hello 데이터 hello에 클레임은 hello 리소스 테 넌 트의 회사 개체에 대 한 속성이 있습니다.
- "변환": hello 데이터 hello에 클레임은 클레임 변환에서 (이 문서의 뒷부분에 나오는 "클레임 변환" hello 섹션 참조). 

Hello 원본이 변환 인 경우 hello **TransformationID** 요소는이 클레임 정의에 포함 되어야 합니다.

hello ID 요소 hello 클레임에 대 한 hello 값을 제공 하는 hello 소스에서 되는 속성을 식별 합니다. hello 다음 표에서 hello 값 id 원본의 각 값에 대해 유효 합니다.

#### <a name="table-3-valid-id-values-per-source"></a>표 3: 원본별 유효한 ID 값
|원본|ID|설명|
|-----|-----|-----|
|사용자|surname|성|
|사용자|givenname|이름|
|사용자|displayname|표시 이름|
|사용자|objectId|ObjectID|
|사용자|mail|메일 주소|
|사용자|userprincipalname|사용자 계정 이름|
|사용자|department|department|
|사용자|onpremisessamaccountname|온-프레미스 SAM 계정 이름|
|사용자|netbiosname|NetBios 이름|
|사용자|dnsdomainname|DNS 도메인 이름|
|사용자|onpremisesecurityidentifier|온-프레미스 보안 식별자|
|사용자|companyname|조직 이름|
|사용자|streetaddress|주소|
|사용자|postalcode|우편 번호|
|사용자|preferredlanguange|기본 설정 언어|
|사용자|onpremisesuserprincipalname|온-프레미스 UPN|
|사용자|mailNickname|메일 애칭|
|사용자|extensionattribute1|확장 특성 1|
|사용자|extensionattribute2|확장 특성 2|
|사용자|extensionattribute3|확장 특성 3|
|사용자|extensionattribute4|확장 특성 4|
|사용자|extensionattribute5|확장 특성 5|
|사용자|extensionattribute6|확장 특성 6|
|사용자|extensionattribute7|확장 특성 7|
|사용자|extensionattribute8|확장 특성 8|
|사용자|extensionattribute9|확장 특성 9|
|사용자|extensionattribute10|확장 특성 10|
|사용자|extensionattribute11|확장 특성 11|
|사용자|extensionattribute12|확장 특성 12|
|사용자|extensionattribute13|확장 특성 13|
|사용자|extensionattribute14|확장 특성 14|
|사용자|extensionattribute15|확장 특성 15|
|사용자|othermail|다른 메일|
|사용자|country|국가|
|사용자|city|City|
|사용자|state|시스템 상태|
|사용자|jobtitle|직위|
|사용자|employeeid|직원 ID|
|사용자|facsimiletelephonenumber|팩스 번호|
|응용 프로그램, 리소스, 대상 그룹|displayname|표시 이름|
|응용 프로그램, 리소스, 대상 그룹|objected|ObjectID|
|응용 프로그램, 리소스, 대상 그룹|tags|서비스 주체 태그|
|회사|tenantcountry|테넌트 국가|

**TransformationID:** hello TransformationID 요소는 소스 요소가 너무 설정 되는 경우에 hello 제공 해야 합니다. "변환"입니다.

- 이 요소에는 hello에 hello 변형 항목의 ID 요소 hello와 일치 해야 **ClaimsTransformation** 이 클레임에 대 한 hello 데이터 생성 되는 방식을 정의 하는 속성입니다.

**클레임 유형:** hello **JwtClaimType** 및 **SamlClaimType** 요소 클레임 스키마 항목이이 참조 하는 클레임을 정의 합니다.

- hello JwtClaimType hello hello 클레임 toobe Jwt에 포함 된 이름을 포함 해야 합니다.
- hello SamlClaimType hello hello의 URI toobe SAML 토큰에 포함 된 클레임을 포함 해야 합니다.

>[!NOTE]
>이름 및 Uri hello에 있는 클레임의 제한 클레임 집합 hello 클레임 형식 요소에 사용할 수 없습니다. 자세한 내용은이 문서의 뒷부분에 나오는 hello "예외 및 제한 사항" 섹션을 참조 합니다.

### <a name="claims-transformation"></a>클레임 변환

**문자열:** ClaimsTransformation

**데이터 형식:** 하나 이상의 변환 항목을 가진 JSON Blob입니다. 

**요약:** toogenerate hello 출력 데이터에 지정 된 클레임에 대 한 hello 클레임 스키마를이 속성 tooapply 일반적인 변환 toosource 데이터를 사용 합니다.

**ID:** 사용 하 여 hello ID 요소 tooreference hello TransformationID 클레임 스키마 항목에서에서이 변환 항목입니다. 이 값은 이 정책 내에서 각 변환 항목에 고유해야 합니다.

**TransformationMethod:** hello TransformationMethod 요소는 작업은 수행된 toogenerate hello 데이터 hello 클레임에 대 한 식별 합니다.

선택한 hello 방법에 따라, 입력 및 출력의 집합을 사용할 수 있습니다. Hello를 사용 하 여 정의 되며 **InputClaims**, **InputParameters** 및 **OutputClaims** 요소입니다.

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>표 4: 변환 메서드 및 예상 입력 및 출력
|TransformationMethod|예상 입력|예상 출력|설명|
|-----|-----|-----|-----|
|Join|string1, string2, 구분 기호|outputClaim|구분 기호를 사용하여 입력 문자열을 조인합니다. 예: string1:"foo@bar.com" , string2:"sandbox" , separator:"."는 outputClaim:"foo@bar.com.sandbox"를 생성합니다.|
|ExtractMailPrefix|mail|outputClaim|Hello 전자 메일 주소의 로컬 부분을 추출합니다. 예: mail:"foo@bar.com"은 outputClaim:"foo"를 생성합니다. @ 하지 않는 경우 부호가 있는, hello 원래 입력된 문자열은 있는 그대로 반환 됩니다.|

**InputClaims:** 는 InputClaims 요소 toopass hello 데이터 클레임 스키마 항목 tooa 변환을를 사용 합니다. 두 개의 특성인 **ClaimTypeReferenceId** 및 **TransformationClaimType**이 있습니다.

- **ClaimTypeReferenceId** hello 클레임 스키마 항목 toofind hello 적절 한 입력된 클레임의 ID 요소와 조인 합니다. 
- **TransformationClaimType** 가 사용 되는 toogive 고유 이름을 toothis 입력 합니다. 이 이름은 hello 변환 방법에 대 한 예상 hello 입력 중 하 나와 일치 해야 합니다.

**InputParameters:** InputParameters 요소 toopass 상수 값 tooa 변환을 사용 합니다. 두 개의 특성인 **Value** 및 **ID**가 있습니다.

- **값** hello 상수 값을 실제 toobe 전달 됩니다.
- **ID** 가 사용 되는 toogive 고유 이름을 toothis 입력 합니다. 이 이름은 hello 변환 방법에 대 한 예상 hello 입력 중 하 나와 일치 해야 합니다.

**OutputClaims:** 변환에서 생성 되는 OutputClaims 요소 toohold hello 데이터를 사용 하 고 tooa 클레임 스키마 항목을 연결 합니다. 두 개의 특성인 **ClaimTypeReferenceId** 및 **TransformationClaimType**이 있습니다.

- **ClaimTypeReferenceId** hello hello 요청 스키마 항목 toofind hello 적절 한 출력 요청 ID와 조인 합니다.
- **TransformationClaimType** 사용된 toogive는 고유한 이름을 toothis 출력 됩니다. 이 이름은 hello 변환 방법에 대 한 예상 hello 출력 중 하나로 일치 해야 합니다.

### <a name="exceptions-and-restrictions"></a>예외 및 제한 사항

**SAML NameID 및 UPN:** hello NameID 및 UPN 값 소스와 hello 클레임 변환을 허용 되는 hello 특성은 제한 됩니다.

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>표 5: SAML NameID에 대한 데이터 원본으로 허용되는 특성
|원본|ID|설명|
|-----|-----|-----|
|사용자|mail|메일 주소|
|사용자|userprincipalname|사용자 계정 이름|
|사용자|onpremisessamaccountname|온-프레미스 SAM 계정 이름|
|사용자|employeeid|직원 ID|
|사용자|extensionattribute1|확장 특성 1|
|사용자|extensionattribute2|확장 특성 2|
|사용자|extensionattribute3|확장 특성 3|
|사용자|extensionattribute4|확장 특성 4|
|사용자|extensionattribute5|확장 특성 5|
|사용자|extensionattribute6|확장 특성 6|
|사용자|extensionattribute7|확장 특성 7|
|사용자|extensionattribute8|확장 특성 8|
|사용자|extensionattribute9|확장 특성 9|
|사용자|extensionattribute10|확장 특성 10|
|사용자|extensionattribute11|확장 특성 11|
|사용자|extensionattribute12|확장 특성 12|
|사용자|extensionattribute13|확장 특성 13|
|사용자|extensionattribute14|확장 특성 14|
|사용자|extensionattribute15|확장 특성 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>표 6: SAML NameID에 허용되는 변환 메서드
|TransformationMethod|제한|
| ----- | ----- |
|ExtractMailPrefix|없음|
|Join|조인 된 hello 접미사 hello 리소스 테 넌 트의 확인 된 도메인 이어야 합니다.|

### <a name="custom-signing-key"></a>사용자 지정 서명 키
사용자 지정 서명 키 toohello 정책 tootake 효과 매핑 클레임에 대 한 서비스 사용자 개체를 할당 되어야 합니다. Hello 정책에 의해 영향을 받았는지는 발급 된 모든 토큰은이 키로 서명 됩니다. 응용 프로그램에 구성 된 tooaccept 토큰이이 키로 서명 해야 합니다. 이렇게 하면 토큰의 hello hello 작성자에 의해 수정 된 승인 클레임 매핑 정책. 이는 악의적인 행위자가 만든 클레임 매핑 정책으로부터 응용 프로그램을 보호합니다.

### <a name="cross-tenant-scenarios"></a>교차 테넌트 시나리오
클레임 정책 매핑 tooguest 사용자가 적용 되지 않습니다. 게스트 사용자가 tooaccess 응용 프로그램을 클레임 매핑 할당 된 정책 tooits 서비스 보안 주체, hello 기본 토큰이 발급 됩니다 (hello 정책은 어떤 영향도 주지).

## <a name="claims-mapping-policy-assignment"></a>클레임 매핑 정책 할당
클레임 매핑 정책은 수만 할당 될 tooservice principal 개체입니다.

### <a name="example-claims-mapping-policies"></a>예제 클레임 매핑 정책

Azure AD에서 특정 서비스 주체에 대해 토큰에 내보내지는 클레임을 사용자 지정할 수 있는 경우 많은 시나리오가 가능합니다. 이 섹션에 살펴보기 toouse hello 매핑 정책 형식을 요구 하는 방법을 이해 하는 데 도움이 되는 몇 가지 일반적인 시나리오입니다.

#### <a name="prerequisites"></a>필수 조건
다음 예제는 hello, 업데이트, 링크를 만들고 서비스 사용자에 대 한 정책을 삭제 합니다. 새 tooAzure AD 인 경우 Azure AD는 tooget 이러한 예제를 진행 하기 전에 테 넌 트에 대 한 자세한 내용은 하는 것이 좋습니다. 

시작 tooget 단계 hello지 않습니다.


1. Hello를 최신 버전 다운로드 [Azure AD PowerShell 모듈 공개 미리 보기 릴리스에서](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127)합니다.
2.  Hello Connect 명령 toosign tooyour Azure AD 관리자 계정에서에서 실행 합니다. 새 세션을 시작할 때마다 이 명령을 실행합니다.
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee 다음 실행된 hello 조직에서 생성 된 모든 정책을 명령입니다. Hello에 대부분의 작업 후이 명령을 실행 하는 것이 좋습니다 toocheck 정책으로 만들고 있는 다음 시나리오를 예상 합니다.
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>예:가 만들고는 정책 tooomit hello 기본의 클레임을 발급 한 토큰 tooa 서비스 사용자를 할당 합니다.
이 예제에서 발급 한 토큰 toolinked hello 기본 클레임 집합을 제거 하는 정책을 서비스 사용자를 만듭니다.


1. 클레임 매핑 정책을 만듭니다. 이 정책에 연결 된 toospecific 서비스 보안 주체 토큰에서 hello 기본 클레임 집합을 제거합니다.
    1. 이 명령을 실행 toocreate hello 정책: 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. 새 정책 및 tooget hello 정책 ObjectId, 다음 실행된 hello 명령을 toosee:
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Hello 정책 tooyour 서비스 사용자를 할당 합니다. 서비스 사용자의 ObjectId tooget hello를 해야합니다. 
    1.  toosee 조직의 모든 서비스 사용자를 Microsoft Graph를 쿼리할 수 있습니다. 또는 Azure AD 그래프 탐색기에서 tooyour Azure AD 계정에에서 로그인 합니다.
    2.  다음 명령을 하 여 서비스 보안 주체를 실행 hello의 ObjectId hello을 사용할 수 있습니다.  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>예: 만들기 및 정책 tooinclude 할당 토큰의에서 클레임을 발급 tooa 서비스 사용자 EmployeeID 및 TenantCountry hello 합니다.
이 예제에서는 hello EmployeeID를 추가 하는 정책을 만들고 TenantCountry tootokens toolinked 서비스 보안 주체를 발급 합니다. hello EmployeeID는 SAML 토큰 및 Jwt 모두에서 hello 이름 클레임 유형으로 내보내집니다. hello TenantCountry hello 국가 클레임 SAML 토큰과 Jwt에 형식으로 내보내집니다. 이 예제에서는 hello 토큰에 설정할 tooinclude hello basic 요구를 계속 실행 합니다.

1. 클레임 매핑 정책을 만듭니다. 이 정책에 연결 된 toospecific 서비스 사용자는 hello EmployeeID 및 TenantCountry 클레임 tootokens를 추가합니다.
    1. 이 명령을 실행 toocreate hello 정책:  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. 새 정책 및 tooget hello 정책 ObjectId, 다음 실행된 hello 명령을 toosee:
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  Hello 정책 tooyour 서비스 사용자를 할당 합니다. 서비스 사용자의 ObjectId tooget hello를 해야합니다. 
    1.  toosee 조직의 모든 서비스 사용자를 Microsoft Graph를 쿼리할 수 있습니다. 또는 Azure AD 그래프 탐색기에서 tooyour Azure AD 계정에에서 로그인 합니다.
    2.  다음 명령을 하 여 서비스 보안 주체를 실행 hello의 ObjectId hello을 사용할 수 있습니다.  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>예: 만들기 및 발급 된 토큰 tooa 서비스 사용자에 클레임 변환을 사용 하는 정책을 할당 합니다.
이 예제에서는 내보내는 사용자 지정 클레임 "JoinedData" tooJWTs toolinked 서비스 보안 주체를 발급 하는 정책을 만들 수 있습니다. 이 클레임 ".sandbox" 인 hello 사용자 개체에 hello extensionattribute1 특성에 저장 된 hello 데이터를 조인 하 여 만든 값을 포함 합니다. 이 예제에서는 hello 토큰에 설정 하는 hello 기본 클레임을 제외 합니다.


1. 클레임 매핑 정책을 만듭니다. 이 정책에 연결 된 toospecific 서비스 사용자는 hello EmployeeID 및 TenantCountry 클레임 tootokens를 추가합니다.
    1. 이 명령을 실행 toocreate hello 정책: 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. 새 정책 및 tooget hello 정책 ObjectId, 다음 실행된 hello 명령을 toosee: 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Hello 정책 tooyour 서비스 사용자를 할당 합니다. 서비스 사용자의 ObjectId tooget hello를 해야합니다. 
    1.  toosee 조직의 모든 서비스 사용자를 Microsoft Graph를 쿼리할 수 있습니다. 또는 Azure AD 그래프 탐색기에서 tooyour Azure AD 계정에에서 로그인 합니다.
    2.  다음 명령을 하 여 서비스 보안 주체를 실행 hello의 ObjectId hello을 사용할 수 있습니다. 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
