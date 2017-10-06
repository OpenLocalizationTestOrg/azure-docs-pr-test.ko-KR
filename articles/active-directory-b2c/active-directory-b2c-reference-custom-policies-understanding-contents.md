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
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>Azure AD B2C hello 정책 사용자 지정 스타터 팩의 사용자 지정 정책 hello 이해

이 섹션에서는 hello와 함께 제공 하는 hello B2C_1A_base 정책의 모든 hello 코어 요소 **스타터 팩** hello의 hello 상속을 통해 직접 정책을 작성에 대 한를 활용 하 고 *B2C_1A_base_ 확장명 정책*합니다.

이와 같이 더 특히 집중적으로 다룹니다 hello 이미 정의 된 클레임 형식, 클레임 변환을, 콘텐츠 정의 클레임 공급자에 게 자신의 기술 프로필 하 고 핵심 사용자 여정이 hello 합니다.

> [!IMPORTANT]
> Microsoft는 어떠한 명시적 이거나 묵시적인 보증도 하지 않습니다이 제공 된 기준 toohello 정보를는. GA 시간 이전, GA 시간 또는 그 이후에 언제든지 변경 사항을 적용할 수 있습니다.

사용자 고유의 정책 및 hello B2C_1A_base_extensions 정책 수 이러한 정의 무시 하 고 필요에 따라 추가 구성을 제공 하 여이 부모 정책을 확장 합니다.

hello의 핵심 요소 hello *B2C_1A_base 정책* 클레임 형식과 클레임 변환을 콘텐츠 정의 됩니다. 이러한 요소에도 hello와 같이 사용자 고유의 정책에서 참조 되는 취약 toobe 수 *B2C_1A_base_extensions 정책*합니다.

## <a name="claims-schemas"></a>클레임 스키마

이 스키마는 다음과 같은 세 가지 섹션으로 구분됩니다.

1.  Hello 최소 데 필요한 클레임을 사용자 여정이 toowork hello에 대 한 제대로 나열 하는 첫 번째 섹션입니다.
2.  두 번째 섹션 목록에 쿼리 문자열 매개 변수가 필요한 클레임 hello 및 기타 특수 매개 변수 toobe 전달 tooother 클레임 공급자 인증을 위해 특히 login.microsoftonline.com입니다. **이러한 클레임을 수정하지 마세요**.
3.  되 고 hello 사용자 로부터 수집할 수 있는 추가, 선택적 클레임을 나열 하는 세 번째 섹션 hello 디렉터리에 저장 하는 동안 로그인 토큰에 전송 합니다. 이 섹션에 유형 toobe hello 사용자 로부터 수집 및/또는 hello 토큰에 전송 하는 새 클레임을 추가할 수 있습니다.

> [!IMPORTANT]
> hello 클레임 스키마 암호와 사용자 이름을 같은 특정 클레임에 대 한 제한을 있습니다. hello 신뢰 프레임 워크 (TF) 정책 다른 클레임 공급자와 Azure AD를 취급 하 고 hello 프리미엄 정책에 해당 하는 모든 제한은 모델링 됩니다. 정책이 수정된 tooadd 더 많은 제한이 또는 고유 제한 사항을 포함 하는 자격 증명 저장소에 대 한 다른 클레임 공급자를 사용 합니다.

아래 hello 사용 가능한 클레임 유형이 나와 있습니다.

### <a name="claims-that-are-required-for-hello-user-journeys"></a>Hello 사용자 친구에 필요한 클레임

다음 클레임 hello가 제대로 사용자 여정이 toowork 필요 합니다.

| 클레임 유형 | 설명 |
|-------------|-------------|
| *UserId* | 사용자 이름 |
| *signInName* | 로그인 이름 |
| *tenantId* | Azure AD B2C 프리미엄에 hello 사용자 개체의 테 넌 트 식별자 (ID) |
| *objectId* | Azure AD B2C 프리미엄에 hello 사용자 개체의 개체 식별자 (ID) |
| *암호* | 암호 |
| *newPassword* | |
| *reenterPassword* | |
| *passwordPolicies* | Azure AD B2C 프리미엄 toodetermine 암호 강도, 만료, 등에서 사용 하는 암호 정책입니다. |
| *sub* | |
| *alternativeSecurityId* | |
| *identityProvider* | |
| *displayName* | |
| *strongAuthenticationPhoneNumber* | 사용자의 전화 번호 |
| *Verified.strongAuthenticationPhoneNumber* | |
| *email* | 전자 메일 주소를 사용 하는 toocontact hello 사용자 일 수 있습니다. |
| *signInNamesInfo.emailAddress* | Hello 사용자 전자 메일 주소에 toosign צ ְ ײ |
| *otherMails* | 사용 되는 toocontact hello 사용자 일 수 있는 전자 메일 주소 |
| *userPrincipalName* | Azure AD B2C 프리미엄 hello에 저장 되어 있는 사용자 이름 |
| *upnUserName* | 사용자 계정 이름을 만들기 위한 사용자 이름 |
| *mailNickName* | Azure AD B2C 프리미엄 hello에 저장 된 사용자의 메일 nick 이름 |
| *newUser* | |
| *executed-SelfAsserted-Input* | 특성 hello 사용자 로부터 수집한 여부를 지정 하는 클레임 |
| *executed-PhoneFactor-Input* | 새 전화 번호를 hello 사용자 로부터 수집 된 있는지 여부를 지정 하는 클레임 |
| *authenticationSource* | Hello 사용자 소셜 Id 공급자, login.microsoftonline.com, 또는 로컬 계정에서 인증 되었는지 여부를 지정 합니다. |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>쿼리 문자열 매개 변수 및 기타 특수 매개 변수에 필요한 클레임

hello 다음 클레임은 특수 한 매개 변수 (일부 쿼리 문자열 매개 변수 포함) tooother 클레임 공급자에 필요한 toopass:

| 클레임 유형 | 설명 |
|-------------|-------------|
| *nux* | 인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달 |
| *nca* | 인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달 |
| *prompt* | 인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달 |
| *mkt* | 인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달 |
| *lc* | 인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달 |
| *grant_type* | 인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달 |
| *scope* | 인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달 |
| *client_id* | 인증 toologin.microsoftonline.com 로컬 계정에 대 한 특별 한 매개 변수 전달 |
| *objectIdFromSession* | SSO 세션에서 검색 된 hello 기본 세션 관리 공급자 tooindicate hello 개체 id는에서 제공 하는 매개 변수 |
| *isActiveMFASession* | 매개 변수는 hello이 사용자는 활성 MFA 세션 hello MFA 세션 관리 tooindicate에서 제공 |

### <a name="additional-optional-claims-that-can-be-collected"></a>수집할 수 있는 추가(또는 선택적) 클레임

hello 다음 클레임은 hello 사용자 로부터 수집할 수 있는 추가 클레임 hello 디렉터리에 저장 된 고 hello 토큰에 전송 합니다. 개략적인 설명 대로 하기 전에, 추가 클레임 toothis 목록을 추가할 수 있습니다.

| 클레임 유형 | 설명 |
|-------------|-------------|
| *givenName* | 사용자의 지정된 이름(이름이라고도 함) |
| *surname* | 사용자의 성(패밀리 이름 또는 성이라고도 함) |
| *Extension_picture* | 소셜에서 사용자의 그림 |

## <a name="claim-transformations"></a>클레임 변환

hello 사용 가능한 클레임 변환은 다음과 같습니다.

| 클레임 변환 | 설명 |
|----------------------|-------------|
| *CreateOtherMailsFromEmail* | |
| *CreateRandomUPNUserName* | |
| *CreateUserPrincipalName* | |
| *CreateSubjectClaimFromObjectID* | |
| *CreateSubjectClaimFromAlternativeSecurityId* | |
| *CreateAlternativeSecurityId* | |

## <a name="content-definitions"></a>콘텐츠 정의

이 섹션에서는 hello에 이미 선언 hello 콘텐츠 정의 설명 *B2C_1A_base* 정책입니다. 이 콘텐츠 정의 참조, 재정의 및/또는 hello와 같이 사용자 고유의 정책에서 필요에 따라 확장 취약 toobe *B2C_1A_base_extensions* 정책입니다.

| 클레임 공급자 | 설명 |
|-----------------|-------------|
| *Facebook* | |
| *로컬 계정 로그인* | |
| *PhoneFactor* | |
| *Azure Active Directory* | |
| *자체 어설션됨* | |
| *로컬 계정* | |
| *세션 관리* | |
| *Trustframework Policy Engine* | |
| *TechnicalProfiles* | |
| *토큰 발급자* | |

## <a name="technical-profiles"></a>기술 프로필

이 섹션에서는 hello에 대 한 클레임 공급자 당 이미 선언 되었습니다. hello 기술 프로필을 보여 줍니다. *B2C_1A_base* 정책입니다. 이러한 기술 프로필은 더 이상 참조, 재정의 및/또는 hello와 같이 사용자 고유의 정책에서 필요에 따라 확장 취약 toobe *B2C_1A_base_extensions* 정책입니다.

### <a name="technical-profiles-for-facebook"></a>Facebook용 기술 프로필

| 기술 프로필 | 설명 |
|-------------------|-------------|
| *Facebook-OAUTH* | |

### <a name="technical-profiles-for-local-account-signin"></a>로컬 계정 로그인용 기술 프로필

| 기술 프로필 | 설명 |
|-------------------|-------------|
| *Login-NonInteractive* | |

### <a name="technical-profiles-for-phone-factor"></a>Phone Factor용 기술 프로필

| 기술 프로필 | 설명 |
|-------------------|-------------|
| *PhoneFactor-Input* | |
| *PhoneFactor-InputOrVerify* | |
| *PhoneFactor-Verify* | |

### <a name="technical-profiles-for-azure-active-directory"></a>Azure Active Directory용 기술 프로필

| 기술 프로필 | 설명 |
|-------------------|-------------|
| *AAD-Common* | 에 의해 포함 되는 기술 프로필 hello 다른 AAD xxx 기술 프로필 |
| *AAD-UserWriteUsingAlternativeSecurityId* | 소셜 로그인용 기술 프로필 |
| *AAD-UserReadUsingAlternativeSecurityId* | 소셜 로그인용 기술 프로필 |
| *AAD-UserReadUsingAlternativeSecurityId-NoError* | 소셜 로그인용 기술 프로필 |
| *AAD-UserWritePasswordUsingLogonEmail* | 로컬 계정을 위한 기술 프로필 |
| *AAD-UserReadUsingEmailAddress* | 로컬 계정을 위한 기술 프로필 |
| *AAD-UserWriteProfileUsingObjectId* | objectId를 사용하여 사용자 레코드 업데이트를 위한 기술 프로필 |
| *AAD-UserWritePhoneNumberUsingObjectId* | objectId를 사용하여 사용자 레코드 업데이트를 위한 기술 프로필 |
| *AAD-UserWritePasswordUsingObjectId* | objectId를 사용하여 사용자 레코드 업데이트를 위한 기술 프로필 |
| *AAD-UserReadUsingObjectId* | 사용자 인증 후 기술 프로필은 tooread 사용 되는 데이터 |

### <a name="technical-profiles-for-self-asserted"></a>자체 어설션용 기술 프로필

| 기술 프로필 | 설명 |
|-------------------|-------------|
| *SelfAsserted-Social* | |
| *SelfAsserted-ProfileUpdate* | |

### <a name="technical-profiles-for-local-account"></a>로컬 계정용 기술 프로필

| 기술 프로필 | 설명 |
|-------------------|-------------|
| *LocalAccountSignUpWithLogonEmail* | |

### <a name="technical-profiles-for-session-management"></a>세션 관리용 기술 프로필

| 기술 프로필 | 설명 |
|-------------------|-------------|
| *SM-Noop* | |
| *SM-AAD* | |
| *SM-SocialSignup* | 프로필 이름은 기호 간에 사용 되는 toodisambiguate AAD 세션 구성 되 고 이며에 로그인 |
| *SM-SocialLogin* | |
| *SM-MFA* | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Trustframework Policy Engine TechnicalProfiles용 기술 프로필

Hello에 대 한 기술 프로필이 정의 된 현재 **Trustframework 정책 엔진 TechnicalProfiles** 클레임 공급자입니다.

### <a name="technical-profiles-for-token-issuer"></a>토큰 발급자용 기술 프로필

| 기술 프로필 | 설명 |
|-------------------|-------------|
| *JwtIssuer* | |

## <a name="user-journeys"></a>사용자 경험

이 섹션에서는 hello에 이미 선언 hello 사용자 친구를 보여 줍니다. *B2C_1A_base* 정책입니다. 이러한 사용자 친구는 더 이상 참조, 재정의 및/또는 hello와 같이 사용자 고유의 정책에서 필요에 따라 확장 취약 toobe *B2C_1A_base_extensions* 정책입니다.

| 사용자 경험 | 설명 |
|--------------|-------------|
| *SignUp* | |
| *SignIn* | |
| *SignUpOrSignIn* | |
| *EditProfile* | |
| *PasswordReset* | |
