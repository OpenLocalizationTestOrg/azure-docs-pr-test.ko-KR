---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 Salesforce SAML 공급자 추가 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 toocreate 및 Azure Active Directory B2C 사용자 지정 정책을 관리 합니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Azure Active Directory B2C: SAML을 통해 Salesforce 계정을 사용하여 로그인

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

이 문서에서는 어떻게 toouse [사용자 지정 정책을](active-directory-b2c-overview-custom.md) tooset 로그인 특정 Salesforce 조직에서 사용자가 합니다.

## <a name="prerequisites"></a>필수 조건

### <a name="azure-ad-b2c-setup"></a>Azure AD B2C 설정

모든 너무 방법을 보여 주는 hello 단계를 완료 했는지 확인 하십시오.[사용자 지정 정책 시작](active-directory-b2c-get-started-custom.md) Azure Active Directory B2C에 (Azure AD B2C).

내용은 다음과 같습니다.

* Azure AD B2C 테넌트 만들기
* Azure AD B2C 응용 프로그램 만들기
* 두 개의 정책 엔진 응용 프로그램 등록
* 키 설정
* Hello 스타터 팩을 설정 합니다.

### <a name="salesforce-setup"></a>Salesforce 설정

이 문서에서는 hello 다음 이미 추가한 가정 합니다.

* Salesforce 계정 등록. [Developer Edition 평가판 계정](https://developer.salesforce.com/signup)에 등록할 수 있습니다.
* Salesforce 조직에 [내 도메인을 설정](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0)합니다.

## <a name="set-up-salesforce-so-users-can-federate"></a>사용자가 페더레이션할 수 있도록 Salesforce 설정

Salesforce와 toohelp Azure AD B2C 통신, tooget hello Salesforce 메타 데이터 URL이 필요 합니다.

### <a name="set-up-salesforce-as-an-identity-provider"></a>Salesforce를 ID 공급자로 설정

> [!NOTE]
> 이 문서에서는 [Salesforce Lightning 환경](https://developer.salesforce.com/page/Lightning_Experience_FAQ)을 사용한다고 가정합니다.

1. [TooSalesforce 로그인](https://login.salesforce.com/)합니다. 
2. Hello 왼쪽 메뉴 아래에서 **설정**를 확장 하 고 **Identity**, 클릭 하 고 **Id 공급자**합니다.
3. **ID 공급자 사용**을 클릭합니다.
4. 아래 **선택 hello 인증서**선택, Azure AD B2C와 Salesforce toouse toocommunicate hello 인증서입니다. (Hello 기본 인증서를 사용할 수 있습니다.) **Save**를 클릭합니다. 

### <a name="create-a-connected-app-in-salesforce"></a>Salesforce에서 연결된 앱 만들기

1. Hello에 **Id 공급자** 페이지에서 이동 너무**서비스 공급자**합니다.
2. **Service Providers are now created via Connected Apps. Click here.**(서비스 공급자가 연결된 앱을 통해 생성됩니다. 여기를 클릭하세요.)를 클릭합니다.
3. 아래 **기본 정보**, 연결 된 앱에 대 한 hello 필요한 값을 입력 합니다.
4. 아래 **웹 앱 설정을**선택, hello **SAML을 사용 하도록 설정** 확인란 합니다.
5. Hello에 **엔터티 ID** 필드 hello url을 입력 합니다. 에 대 한 hello 값 바꾸어야 `tenantName`합니다.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. Hello에 **ACS URL** 필드 hello url을 입력 합니다. 에 대 한 hello 값 바꾸어야 `tenantName`합니다.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. 다른 모든 설정에 대 한 hello 기본값 그대로 둡니다.
8. Hello 목록의 toohello 아래쪽 스크롤한 다음 클릭 **저장**합니다.

### <a name="get-hello-metadata-url"></a>Hello 메타 데이터 URL 가져오기

1. 연결 된 응용 프로그램의 hello 개요 페이지에서 클릭 **관리**합니다.
2. Hello 값을 복사 **메타 데이터 검색 끝점**를 저장 합니다. 이 문서의 뒷부분에서 사용합니다.

### <a name="set-up-salesforce-users-toofederate"></a>Salesforce 사용자 toofederate 설정

1. Hello에 **관리** 페이지 연결 된 응용 프로그램의 이동 너무**프로필**합니다.
2. **프로필 관리**를 클릭합니다.
3. Hello 프로필 (또는 사용자 그룹을) 선택와 Azure AD B2C toofederate 되도록 합니다. 시스템 관리자로 hello 선택 **시스템 관리자에 게** 확인란 Salesforce 계정을 사용 하 여 페더레이션 할 수 있도록 합니다.

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>Azure AD B2C에 대한 서명 인증서 생성

요청은 Azure AD B2C 서명한 tooSalesforce 필요 toobe를 전송 합니다. toogenerate 서명 인증서를 Azure PowerShell을 열고 hello 다음 명령을 실행 합니다.

> [!NOTE]
> Hello 상위 두 줄에 hello 테 넌 트 이름 및 암호를 업데이트 하 고 있는지 확인 합니다.

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>Hello SAML 서명 인증서 tooAzure AD B2C 추가

서명 인증서 tooyour Azure AD B2C 테 넌 트 hello를 업로드 합니다. 

1. Tooyour Azure AD B2C 테 넌 트를 이동 합니다. **설정** > **ID 환경 프레임워크** > **정책 키**를 클릭합니다.
2. **+추가**를 클릭한 다음
    1. **옵션** > **업로드**를 클릭합니다.
    2. **이름**을 입력합니다(예: SAMLSigningCert). hello 접두사 *B2C_1A_* 키의 toohello 이름을 자동으로 추가 됩니다.
    3. tooselect 인증서를 선택 **업로드 파일 컨트롤**합니다. 
    4. Hello PowerShell 스크립트에서 설정한 hello 인증서의 암호를 입력 합니다.
3. **만들기**를 클릭합니다.
4. 키를 만들었는지 확인합니다(예: B2C_1A_SAMLSigningCert). 전체 이름 hello 기록해 둡니다 (포함 하 여 *B2C_1A_*). Hello 정책의 뒷부분에 나오는 toothis 키를 참조 합니다.

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>기본 정책에서 hello Salesforce SAML 클레임 공급자 만들기

Salesforce를 사용 하 여 사용자가 로그인 할 수 있도록 Salesforce toodefine를 클레임 공급자로 필요 합니다. 즉, Azure AD B2C 통신할 toospecify hello 끝점을 해야 합니다. hello 끝점은 *제공* 집합이 *클레임* Azure AD B2C tooverify 특정 사용자가 자신을 인증을 사용 합니다. toodo이 추가 `<ClaimsProvider>` 정책 hello 확장 파일에서 Salesforce에 대 한:

1. 작업 디렉터리에서 hello 확장 파일 (TrustFrameworkExtensions.xml)를 엽니다.
2. Hello `<ClaimsProviders>` 섹션. 존재 하지 않는 경우 hello 루트 노드에 만듭니다.
3. 새 `<ClaimsProvider>`을 추가합니다.

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

Hello에서 `<ClaimsProvider>` 노드:

1. Hello 값에 대 한 변경 `<Domain>` 구별 하는 고유한 값 tooa `<ClaimsProvider>` 기타 id 공급자에서 합니다.
2. 에 대 한 hello 시간 `<DisplayName>` hello에 대 한 tooa 표시 이름 클레임 공급자입니다. 이 값은 현재 사용되지 않습니다.

### <a name="update-hello-technical-profile"></a>Hello 기술 프로필 업데이트

tooget Salesforce에서 SAML 토큰을 Azure AD B2C ´ ֲ toocommunicate Azure Active Directory (Azure AD)와 hello 프로토콜을 정의 합니다. Hello에서 이렇게 `<TechnicalProfile>` 요소의 `<ClaimsProvider>`:

1. 업데이트의 hello hello ID `<TechnicalProfile>` 노드. 이 ID가 사용 되는 toorefer toothis hello 정책의 다른 부분과에서 기술 프로필.
2. 에 대 한 hello 시간 `<DisplayName>`합니다. 이 값은 로그인 페이지에 hello 로그인 단추에 표시 됩니다.
3. 에 대 한 hello 시간 `<Description>`합니다.
4. Salesforce는 hello SAML 2.0 프로토콜을 사용합니다. 에 대 한 해당 hello 값 확인 `<Protocol>` 은 **SAML2**합니다.

업데이트 hello `<Metadata>` hello 특정 Salesforce 계정에 대 한 XML tooreflect hello 설정을 앞의 섹션입니다. XML hello에서 hello 메타 데이터 값을 업데이트 합니다.

1. Hello 값을 업데이트 `<Item Key="PartnerEntity">` 앞에서 복사한 hello Salesforce 메타 데이터 URL로 합니다. 형식에 따라 hello 다음과 같습니다. 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. Hello에 `<CryptographicKeys>` 섹션의 두 인스턴스에 대 한 업데이트 hello 값 `StorageReferenceId` toohello 이름 서명 인증서 (예를 들어 B2C_1A_SAMLSigningCert)의 hello 키입니다.

### <a name="upload-hello-extension-file-for-verification"></a>확인에 대 한 hello 확장 파일 업로드

정책에는 이제 Azure AD B2C 알 수 있도록 구성 되었습니다 어떻게 salesforce toocommunicate 합니다. 정책 되지 않게 문제 지금까지 tooverify hello 확장 파일을 업로드 하십시오. 정책 tooupload hello 확장 파일:

1. Azure AD B2C 테 넌 트에 toohello 이동 **모든 정책** 블레이드입니다.
2. 선택 hello **있으면 hello 정책 덮어쓰기** 확인란 합니다.
3. Hello 확장 파일 (TrustFrameworkExtensions.xml)를 업로드 합니다. 유효성 검사를 실패하지 않았는지 확인합니다.

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>Salesforce SAML 클레임 공급자의 tooa 사용자 여행 hello 등록

다음으로 사용자 친구의 Salesforce SAML identity provider tooone hello를 추가 합니다. 이 시점에서 hello id 공급자 설정 되어 있지만 hello 사용자 등록 또는 로그인 페이지에서 사용할 수 없는 합니다. 먼저 tooadd hello id 공급자 tooa 로그인 페이지에서 기존 템플릿 사용자 여행의 복제본을 만듭니다. 그런 다음 hello Azure AD id 공급자를 포함 하므로 hello 템플릿을 수정 합니다.

1. Hello 정책 (예를 들어 TrustFrameworkBase.xml)의 기본 파일을 엽니다.
2. Hello `<UserJourneys>` 요소 및 전체 복사 hello `<UserJourney>` , 값 = "SignUpOrSignIn" Id를 포함 합니다.
3. Hello 확장 파일 (예를 들어 TrustFrameworkExtensions.xml)를 엽니다. Hello `<UserJourneys>` 요소입니다. Hello 요소가 존재 하지 않는 경우 만듭니다.
4. 붙여넣기 hello 전체 복사 `<UserJourney>` hello의 자식으로 `<UserJourneys>` 요소입니다.
5. 새 hello의 hello ID 이름 바꾸기 `<UserJourney>` (예를 들어 SignUpOrSignUsingContoso).

### <a name="display-hello-identity-provider-button"></a>디스플레이 hello identity provider 단추

hello `<ClaimsProviderSelection>` 요소는 등록 또는 로그인 페이지에 유사한 tooan identity provider 단추입니다. 추가 하 여 프로그램 `<ClaimsProviderSelection>` toothis 페이지 이동할 때 Salesforce에 대 한 요소를 새 단추가 나타납니다. toodisplay hello identity provider 단추:

1. Hello에 `<UserJourney>` hello, 만든 `<OrchestrationStep>` 와 `Order="1"`합니다.
2. 다음과 같은 XML hello를 추가 합니다.

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. 설정 `TargetClaimsExchangeId` tooa 논리 값입니다. 다음 hello 동일한 것이 좋습니다 다른 사용자와 규칙 (예를 들어  *\[ClaimProviderName\]Exchange*).

### <a name="link-hello-identity-provider-button-tooan-action"></a>링크 hello identity provider 단추 tooan 동작

Identity provider 단추 준비에서를 tooan 작업을 연결 합니다. 이 경우 Azure AD B2C toocommunicate와 Salesforce tooreceive SAML 토큰에 대 한 hello 동작이입니다. 수행할 수 있습니다이 Salesforce SAML에 대 한 기술 hello 프로필에 연결 하 여 클레임 공급자.

1. Hello에 `<UserJourney>` 노드, 찾기 hello `<OrchestrationStep>` 와 `Order="2"`합니다.
2. 다음과 같은 XML hello를 추가 합니다.

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. 업데이트 `Id` toohello 동일한 값에 대 한 이전 사용 `TargetClaimsExchangeId`합니다.
4. 업데이트 `TechnicalProfileReferenceId` toohello `Id` hello 기술의 프로필 앞에서 만든 (예를 들어 ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Hello 업데이트 된 확장 파일 업로드

Hello 확장 파일을 수정 하 고 수행 됩니다. 이 파일을 저장하고 업로드합니다. 모든 유효성 검사에 성공했는지 확인합니다.

### <a name="update-hello-relying-party-file"></a>Hello 신뢰 당사자 파일 업데이트

다음으로 만든 hello 사용자 작업을 시작 하는 hello 신뢰 하는 파티 (RP) 파일을 업데이트 합니다.

1. 작업 디렉터리에서 SignUpOrSignIn.xml의 복사본을 만듭니다. 그런 다음 이름을 바꿉니다(예: SignUpOrSignInWithAAD.xml).
2. 열기 hello 새 파일 및 업데이트 hello `PolicyId` 특성 `<TrustFrameworkPolicy>` 고유 값으로. 정책 (예를 들어 SignUpOrSignInWithAAD) hello 이름입니다.
3. Hello 수정 `ReferenceId` 특성 `<DefaultUserJourney>` toomatch hello `Id` hello 새 사용자의 여행 (예: SignUpOrSignUsingContoso) 생성의 합니다.
4. 변경 내용을 저장 하 고 hello 파일을 업로드 합니다.

## <a name="test-and-troubleshoot"></a>테스트 및 문제 해결

hello Azure 포털에서에서 방금 업로드 tootest hello 사용자 지정 정책 toohello 정책 블레이드에서 이동한 다음 클릭 **지금 실행**합니다. 실패한 경우 [사용자 지정 정책 문제 해결](active-directory-b2c-troubleshoot-custom.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

피드백을 너무 제공[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)합니다.
