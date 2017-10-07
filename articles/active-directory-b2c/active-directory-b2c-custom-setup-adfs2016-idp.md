---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SAML ID 공급자로 ADFS 추가"
description: "SAML 프로토콜 및 사용자 지정 정책을 사용 하 여 ADFS 2016 설정에 대 한 방법 tooarticle"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: 사용자 지정 정책을 사용하여 SAML ID 공급자로 ADFS 추가

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

이 문서에서는 어떻게 tooenable 로그인 hello 사용 하 여 ADFS 계정에서 사용자에 대 한 [사용자 지정 정책을](active-directory-b2c-overview-custom.md)합니다.

## <a name="prerequisites"></a>필수 조건

Hello에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md) 문서.

이러한 단계는 다음과 같습니다.

1.  ADFS 신뢰 당사자 트러스트 만들기
2.  Hello ad FS 신뢰 당사자 트러스트 인증서 tooAzure AD B2C를 추가 합니다.
3.  클레임 공급자 tooa 정책을 추가 합니다.
4.  등록 hello ADFS 계정 공급자 tooa 사용자 여행을 클레임입니다.
5.  업로드 hello 정책 tooan Azure AD B2C 테 넌 트을 테스트할 수도 있습니다.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate 클레임 인식 신뢰 당사자 트러스트

ADFS toouse (Azure AD) Azure Active Directory B2C에는 id 공급자는 ad FS 신뢰 당사자 트러스트 toocreate 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다.

tooadd hello AD FS 관리 스냅인을 사용 하 여 신뢰 하 고 hello 설정을 수동으로 구성 하는 새 신뢰 당사자 페더레이션 서버에서 절차를 수행 하는 hello를 수행 합니다.

멤버 자격이 **관리자**, 또는 이와 동등한 hello 로컬 컴퓨터에 최소 필수 toocomplete hello이이 절차입니다. Hello 적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  서버 관리자에서 **도구**를 클릭하고 **ADFS 관리**를 선택합니다.

2.  **신뢰 당사자 트러스트 추가**를 클릭합니다.
    ![신뢰 당사자 트러스트 추가](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  Hello에 **시작** 페이지에서 선택 **클레임 인식** 클릭 **시작**합니다.
    ![Hello 시작 페이지에서 클레임 인식 선택](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  Hello에 **데이터 원본 선택** 페이지 **hello 신뢰 당사자에 대 한 데이터를 직접 입력**, 클릭 하 고 **다음**합니다.
    ![Hello 신뢰 당사자 트러스트 데이터 입력](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  Hello에 **표시 이름 지정** 페이지에 이름을 입력 합니다 **표시 이름**아래 **메모** 이 신뢰 당사자 트러스트에 대 한 설명을 입력 한 다음 클릭 **다음** .
    ![표시 이름 및 메모 지정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  선택 사항입니다. 있는지 선택적 토큰 암호화 인증서를 다음 hello에 **인증서 구성** 페이지 **찾아보기** toolocate 인증서 파일을 클릭 한 다음 **다음** .
    ![인증서 구성](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  Hello에 **URL 구성** 페이지, 선택 hello **hello SAML 2.0 WebSSO 프로토콜에 대 한 지원을 사용 하도록 설정** 확인란 합니다. 아래 **신뢰 당사자 SAML 2.0 SSO 서비스 URL**이 신뢰 당사자 트러스트에 대 한 hello SAML Security Assertion Markup Language () 서비스 끝점 URL을 입력 한 다음, **다음**합니다.  Hello에 대 한 **신뢰 당사자 SAML 2.0 SSO 서비스 URL**, hello 붙여 `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`합니다. 테 넌 트의 이름 (예를 들어 contosob2c.onmicrosoft.com)으로 {tenant}를 대체 하 고 확장명 정책 이름 (예를 들어 B2C_1A_TrustFrameworkExtensions)으로 hello {정책}를 바꿉니다.
    > [!IMPORTANT]
    >hello 정책 이름은 signup_or_signin 정책에서 상속한,이 경우 하나 hello: `B2C_1A_TrustFrameworkExtensions`합니다.
    >예를 들어 hello URL 일 수 없습니다: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**합니다.

    ![신뢰 당사자 SAML 2.0 SSO 서비스 URL](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. Hello에 **식별자 구성** 페이지에서 지정 하는 hello hello 이전 단계와 동일한 URL을 클릭 **추가** tooadd 해당 toohello 목록으로 이동한 다음 클릭 **다음**합니다.
    ![신뢰 당사자 트러스트 식별자](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  Hello에 **액세스 제어 정책 선택** 정책을 선택 하 고 클릭 **다음**합니다.
    ![액세스 제어 정책 선택](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  Hello에 **tooAdd 신뢰 준비** 페이지 hello 설정을 검토 한 다음 클릭 **다음** toosave 신뢰 당사자 트러스트 정보입니다.
    ![신뢰 당사자 트러스트 정보 저장](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  Hello에 **마침** 페이지를 클릭 **닫기**,이 작업은 자동으로 hello 표시 **클레임 규칙 편집** 대화 상자.
    ![클레임 규칙 편집](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. **규칙 추가**를 클릭합니다.  
      ![새 규칙 추가](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  **클레임 규칙 템플릿**에서 **LDAP 특성을 클레임으로 전송**을 선택합니다.
    ![LDAP 특성을 클레임 템플릿 규칙으로 전송 선택](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  **클레임 규칙 이름**을 제공합니다. Hello에 대 한 **특성 저장소** 선택 **Active Directory 선택** hello 다음 클레임을 추가한 후 클릭 **마침** 및 **확인**합니다.
    ![규칙 속성 설정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  서버 관리자에서 선택 **신뢰 당사자 트러스트** 만든 hello 신뢰 당사자 트러스트를 선택 하 고 클릭 **속성**합니다.
    ![신뢰 당사자 편집 속성](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  신뢰 당사자 트러스트 (B2C 데모) 속성 창을 클릭 hello 하나 **서명** 탭을 클릭 **추가**합니다.  
    ![서명 설정](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  서명 인증서를 추가합니다(개인 키 없는 .cert 파일).  
    ![서명 인증서 추가](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  Hello 신뢰 당사자 트러스트 (B2C 데모) 속성 창에서 클릭 **고급** 탭 하 고 hello 변경 **보안 해시 알고리즘** 너무**s h A-1**, 클릭 **확인**.  
    ![보안 해시 알고리즘 tooSHA-1을 설정 합니다.](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Hello ADFS 계정 응용 프로그램 키 tooAzure AD B2C 추가
ADFS 계정으로 페더레이션 hello 응용 프로그램을 대신 하 여 ADFS 계정 tootrust Azure AD B2C에 대 한 클라이언트 암호에 필요 합니다. Toostore ADFS 인증서에에서 필요한 Azure AD B2C 테 넌 트입니다. 

1.  Tooyour Azure AD B2C 테 넌 트를 이동 하 고 선택 **B2C 설정** > **Id 경험 프레임 워크**
2.  선택 **정책 키** 테 넌 트에 사용할 수 있는 tooview hello 키입니다.
3.  **+추가**를 클릭합니다.
4.  **옵션**에는 **업로드**를 사용합니다.
5.  **이름**에는 `ADFSSamlCert`를 사용합니다.  
    hello 접두사 `B2C_1A_` 자동으로 추가 될 수도 있습니다.
6.  Hello 파일 업로드에서 * * 개인 키가 있는 인증서.pfx 파일을 선택 합니다. 참고:이 인증서 (개인 키 포함 hello) hello 발급 한 hello ad FS 신뢰 당사자에 대해 사용 된 동일한 것 이어야 합니다.
![정책 키 업로드](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  **만들기**
8.  Hello 키를 만든 확인 `B2C_1A_ADFSSamlCert`합니다.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>확장 정책에서 클레임 공급자 추가
ADFS 계정을 사용 하 여 사용자가 toosign에서 원하는 클레임 공급자로 toodefine ADFS 계정이 필요 합니다. 즉, Azure AD B2C와 통신 하는 끝점 toospecify를 해야 합니다. hello 끝점은 특정 사용자가 인증 하는 Azure AD B2C tooverify에서 사용 되는 클레임 집합을 제공 합니다.

확장 정책 파일에서 `<ClaimsProvider>` 노드를 추가하여 ADFS를 클레임 공급자로 정의합니다.

1. 작업 디렉터리부터 hello 확장명 정책 파일 (TrustFrameworkExtensions.xml)을 엽니다. XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).
2. Hello `<ClaimsProviders>` 섹션
3. Hello hello 아래 XML 조각 다음 추가 `ClaimsProviders` 요소 및 바꾸기 `identityProvider` (임의 값 도메인을 나타내는), dns 및 hello 파일을 저장 합니다. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Hello ADFS 계정 클레임 공급자 tooSign를 등록 하거나 사용자의 여행 로그인
이 시점에서 hello id 공급자 설정이 있습니다.  그러나, hello 로그-up/로그인 화면 중에서 가능 하지 않습니다. 이제 tooadd hello ADFS 계정 id 공급자 tooyour 사용자 필요한 `SignUpOrSignIn` 사용자 여행 합니다. toomake 기존 템플릿 사용자 여행 중복 만듭니다 사용할 수 있는 것입니다.  다음, 우리 수정 hello ADFS id 공급자를 포함 하도록 합니다.
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Hello 정책 (예를 들어 TrustFrameworkBase.xml)의 기본 파일을 엽니다.
2.  Hello `<UserJourneys>` 의 요소와 복사 hello 전체 내용을 `<UserJourneys>` 노드.
3.  Hello 확장 파일 (예를 들어 TrustFrameworkExtensions.xml)를 열고 hello `<UserJourneys>` 요소입니다. 존재 하지 않으면 hello 요소 하나를 추가 합니다.
4.  전체 내용을 hello `<UserJournesy>` hello의 자식으로 복사한 노드 `<UserJourneys>` 요소입니다.

### <a name="display-hello-button"></a>디스플레이 hello 단추
hello `<ClaimsProviderSelections>` 요소 hello 클레임 공급자 선택 옵션 목록 및 해당 순서를 정의 합니다.  `<ClaimsProviderSelection>`요소는 로그-up/로그인 페이지에 유사한 tooan identity provider 단추입니다. 추가 하는 경우는 `<ClaimsProviderSelection>` ADFS 계정에 대 한 요소, 사용자 hello 페이지에 처음 삽입 새 단추 표시 합니다. tooadd이이 요소:

1.  Hello `<UserJourney>` 포함 된 노드 `Id="SignUpOrSignIn"` 복사한 hello 사용자 여정에서 합니다.
2.  Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`
3.  `<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>링크 hello 단추 tooan 동작

Toolink 필요한 위치에 있는 단추를가지고 그 tooan 동작 합니다. hello 동작이 경우 ADFS 계정 tooreceive와 Azure AD B2C toocommunicate에 대 한 토큰입니다. ADFS 계정 클레임 공급자에 대 한 hello 기술 프로필을 연결 하 여 hello 단추 tooan 동작을 연결할:

1.  Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.
2.  `<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Hello 확인 `Id` 의과 같은 값인 hello에 `TargetClaimsExchangeId` hello 섹션 앞에 있습니다.
> * 확인 `TechnicalProfileReferenceId` 이전 (Contoso SAML2)를 만든 toohello 기술 프로필 설정 됩니다.

## <a name="upload-hello-policy-tooyour-tenant"></a>Hello 정책 tooyour 테 넌 트에 업로드
1.  Hello에 [Azure 포털](https://portal.azure.com), hello를 전환 [Azure AD B2C 테 넌 트의 상황에 맞는](active-directory-b2c-navigate-to-b2c-context.md), 및 열기 hello **Azure AD B2C** 블레이드입니다.
2.  **ID 경험 프레임워크**를 선택합니다.
3.  열기 hello **모든 정책** 블레이드입니다.
4.  **정책 업로드**를 선택합니다.
5.  확인 **있으면 hello 정책 덮어쓰기** 상자입니다.
6.  **업로드** TrustFrameworkExtensions.xml hello 유효성 검사가 발생 하지 않도록 하 고

## <a name="test-hello-custom-policy-by-using-run-now"></a>지금 실행에 사용 하 여 hello 사용자 지정 정책 테스트
1.  열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.
2.  열기 **B2C_1A_signup_signin**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다. **지금 실행**을 선택합니다.
3.  ADFS 계정을 사용 하 여 수 toosign 있어야 합니다.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[선택 사항] Hello ADFS 계정 클레임 공급자의 tooProfile 편집 사용자 여행 등록
좋습니다 tooadd hello ADFS 계정 id 공급자도 tooyour 사용자 `ProfileEdit` 사용자 여행 합니다. toomake 마지막 두 단계 hello 반복 사용할 수 있습니다.

### <a name="display-hello-button"></a>디스플레이 hello 단추
1.  정책 (예를 들어 TrustFrameworkExtensions.xml) hello 확장 파일을 엽니다.
2.  Hello `<UserJourney>` 포함 된 노드 `Id="ProfileEdit"` 복사한 hello 사용자 여정에서 합니다.
3.  Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`
4.  `<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>링크 hello 단추 tooan 동작
1.  Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.
2.  `<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>지금 실행에 사용 하 여 hello 사용자 지정 프로필 편집 정책 테스트
1.  열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.
2.  열기 **B2C_1A_ProfileEdit**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다. **지금 실행**을 선택합니다.
3.  ADFS 계정을 사용 하 여 수 toosign 있어야 합니다.

## <a name="download-hello-complete-policy-files"></a>Hello 완성 된 정책 파일을 다운로드
선택 사항: 권장 hello 사용자 지정 정책을 사용 하 여 시작 안내를 완료 한 후 사용자 고유의 사용자 지정 정책 파일을 사용 하 여 시나리오를 작성 합니다. [참조 전용 정책 샘플 파일](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
