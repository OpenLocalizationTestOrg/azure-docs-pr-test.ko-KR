---
title: "Azure Active Directory B2C: 사용자 지정 정책에서 등록 수정 및 자체 어설션된 공급자 구성"
description: "추가 연습 toosign를 클레임 및 hello 사용자 입력을 구성 합니다."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a>Azure Active Directory B2C: tooadd 새 클레임 등록을 수정 하 고 사용자 입력을 구성 합니다.

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

이 문서에서 새 사용자가 제공한 항목 (클레임) tooyour signup 사용자 작업을 추가 합니다.  드롭다운을으로 hello 항목을 구성 하 고 필요한 경우 정의 됩니다.

Sipi tootrigger 테스트 전달 하 여 편집 합니다.

## <a name="prerequisites"></a>필수 조건

* Hello 문서에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md)합니다.  Hello 등록/signin 사용자 여행 toosignup 새로운 로컬 계정을 계속 진행 하기 전에 테스트 합니다.


사용자로부터 초기 데이터 수집은 등록/로그인을 통해 수행합니다.  프로필 편집 사용자 경험을 통해 추가 클레임을 나중에 수집할 수 있습니다. Azure AD B2C를 대화형으로 hello 사용자 로부터 직접 정보 수집, 언제 든 지 hello Id 경험 프레임 워크 사용 하 여 해당 `selfasserted provider`합니다. hello 단계 아래에이 공급자를 사용할 때 적용 됩니다.


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a>Hello 클레임, 표시 이름 및 hello 사용자 입력 유형 정의 합니다.
해당 도시에 대 한 hello 사용자에 게 확인 수 있습니다.  다음 요소 toohello hello 추가 `<ClaimsSchema>` hello TrustFrameWorkExtensions 정책 파일의 요소:

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
추가 선택 항목이 클레임 toocustomize hello 여기 만들 수 있습니다.  전체 스키마에 대 한 참조 toohello **Id 경험 프레임 워크 기술 참조 가이드**합니다.  이 가이드는 hello 참조 섹션에 곧 발표 될 예정입니다.

* `<DisplayName>`사용자 용 hello를 정의 하는 문자열은 *레이블*

* `<UserHelpText>`hello 사용자를 필요한 것을 이해 하는 데 도움이 됩니다.

* `<UserInputType>`가 hello 다음 네 가지 옵션 아래에 강조 표시 합니다.
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * `RadioSingleSelectduration` - 단일 선택을 적용합니다.
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * `DropdownSingleSelect`-유효한 값만 hello 선택할을 수 있습니다.

![드롭다운 옵션의 스크린샷](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* `CheckboxMultiSelect`하나 이상의 값 hello 선택할 수 있습니다.

![다중 선택 옵션의 스크린샷](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a>Hello 클레임 toohello 기호 위쪽/여행 사용자 로그인 추가

1. Hello 클레임으로 추가 `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (hello TrustFrameworkBase 정책 파일에 있는).  Note이 TechnicalProfile SelfAssertedAttributeProvider hello를 사용 합니다.

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, toobe collected from hello user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. 으로 hello 클레임 toohello AAD UserWriteUsingLogonEmail 추가 `<PersistedClaim ClaimTypeReferenceId="city" />` hello 사용자 로부터 수집한 후 toowrite hello 클레임 toohello AAD 디렉터리입니다. 하지 toopersist hello 클레임 hello 디렉터리에 나중에 사용할 선호 하는 경우이 단계를 건너뛸 수 있습니다.

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. Hello 클레임 toohello TechnicalProfile 사용자로 로그인 할 때 hello 디렉터리에서 읽을 수 있는 추가 프로그램`<OutputClaim ClaimTypeReferenceId="city" />`

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. Hello 추가 `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP 정책 파일 SignUporSignIn.xml 하므로이 클레임 사용자 성공 여행 후 hello 토큰에 toohello 응용 프로그램에 전달 됩니다.

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-hello-custom-policy-using-run-now"></a>"Run Now"를 사용 하 여 hello 사용자 지정 정책 테스트

1. 열기 hello **Azure AD B2C 블레이드** 너무 이동**Id 경험 프레임 워크 > 사용자 지정 정책의**합니다.
2. 업로드 하는 hello 사용자 지정 정책을 선택 하 고 hello 클릭 **지금 실행** 단추입니다.
3. 전자 메일 주소를 사용 하 여 수 toosign 있어야 합니다.

테스트 모드에서 hello 등록 화면 비슷한 toothis 같아야 합니다.

![수정된 등록 옵션의 스크린샷](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  hello 토큰 백 tooyour 응용 프로그램은 이제 포함 hello `city` 아래 표시 된 대로 클레임
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a>선택 사항: 등록 경험에서 전자 메일 확인 제거

tooskip 전자 메일 확인 hello 정책 작성자 tooremove를 선택할 수 `PartnerClaimType="Verified.Email"`합니다. hello 전자 메일 주소는 필요한 되지만 유효성을 검사 하지 않으면 "Required" = true 제거 됩니다.  이 옵션이 사용자의 사용 사례에 적합한지 신중하게 고려하세요.

Hello에서 기본적으로 전자 메일 활성화가 확인 `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` hello 스타터 팩에서 hello TrustFrameworkBase 정책 파일에:
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a>다음 단계

아래에 나열 된 TechnicalProfiles hello를 변경 하 여 소셜 계정 로그인에 대 한 hello 새 클레임 toohello 흐름을 추가 합니다. 로케이터 hello hello alternativeSecurityId 사용 하 여 hello 사용자 데이터를 읽을 고 사회/페더레이션 계정 로그인 toowrite에서 사용 됩니다.
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
