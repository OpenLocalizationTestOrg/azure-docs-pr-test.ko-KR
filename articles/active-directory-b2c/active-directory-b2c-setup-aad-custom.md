---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 Azure AD 공급자 추가 | Microsoft Docs"
description: "Azure Active Directory B2C 사용자 지정 정책에 대해 알아봅니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Azure Active Directory B2C: Azure AD 계정을 사용하여 로그인

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

이 문서에서는 어떻게 tooenable 로그인 hello 사용을 통해 특정 Azure Active Directory (Azure AD) 조직의 사용자에 대 한 [사용자 지정 정책을](active-directory-b2c-overview-custom.md)합니다.

## <a name="prerequisites"></a>필수 조건

Hello에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md) 문서.

이러한 단계는 다음과 같습니다.

1. Azure AD B2C(Azure Active Directory B2C) 테넌트 만들기
2. Azure AD B2C 응용 프로그램 만들기
3. 두 개의 정책 엔진 응용 프로그램 등록
4. 키 설정
5. Hello 스타터 팩을 설정 합니다.

## <a name="create-an-azure-ad-app"></a>Azure AD 앱 만들기

tooenable 로그인 특정 사용자에 대 한 Azure AD 조직 tooregister hello 조직 Azure AD 테 넌 트 내에서 응용 프로그램을 사용 해야 합니다.

>[!NOTE]
> Hello 조직 Azure AD 테 넌 트 및 "fabrikamb2c.onmicrosoft.com"에 대 한 "contoso.com" 지침을 진행 하는 hello에 hello Azure AD B2C 테 넌 트로 사용 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
1. Hello 위쪽 막대에서 계정을 선택 합니다. Hello에서 **디렉터리** 목록 tooregister 원하는 hello 조직 Azure AD 테 넌 트 응용 프로그램 (contoso.com)을 선택 합니다.
1. 선택 **더 많은 서비스** hello 왼쪽된 창에서 "응용 프로그램 등록 합니다."에 대 한 검색
1. **새 응용 프로그램 등록**을 선택합니다.
1. 응용 프로그램의 이름(예: `Azure AD B2C App`)을 입력합니다.
1. 선택 **웹 응용 프로그램 / API** hello 응용 프로그램 종류에 대 한 합니다.
1. 에 대 한 **로그온 URL**, hello url을 입력 합니다. 여기서 `yourtenant` Azure AD B2C 테 넌 트의 hello 이름으로 바뀝니다 (`fabrikamb2c.onmicrosoft.com`):

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Save hello 응용 프로그램 id입니다.
1. 새로 만든 hello 응용 프로그램을 선택 합니다.
1. Hello에서 **설정** 블레이드를 **키**합니다.
1. 새 키를 만들고 저장합니다. Hello 다음 섹션의 hello 단계에서 사용 합니다.

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>Azure AD hello 키 tooAzure AD B2C 추가

Azure AD B2C 테 넌 트의 toostore hello contoso.com 응용 프로그램 키가 필요 합니다. toodo이:
1. Tooyour Azure AD B2C 테 넌 트를 이동 하 고 선택 **B2C 설정** > **Id 경험 프레임 워크** > **정책 키**합니다.
1. **+추가**를 선택합니다.
1. 다음 옵션을 선택하거나 입력합니다.
   * **수동**을 선택합니다.
   * **이름**에 대해 Azure AD 테넌트 이름과 일치하는 이름(예: `ContosoAppSecret`)을 선택합니다.  hello 접두사 `B2C_1A_` 키의 toohello 이름을 자동으로 추가 합니다.
   * Hello에 응용 프로그램에 키 붙여넣기 **비밀** 상자입니다.
   * **서명**을 선택합니다.
1. **만들기**를 선택합니다.
1. Hello 키를 만든 확인 `B2C_1A_ContosoAppSecret`합니다.


## <a name="add-a-claims-provider-in-your-base-policy"></a>기본 정책에서 클레임 공급자 추가

Azure AD를 사용 하 여 사용자가 toosign의 하려는 경우 Azure AD를 클레임 공급자로 toodefine를 해야 합니다. 즉, Azure AD B2C와 통신 하는 끝점 toospecify를 해야 합니다. hello 끝점에서 특정 사용자가 인증 하는 Azure AD B2C tooverify 사용 되는 클레임 집합을 제공 합니다. 

Azure AD toohello를 추가 하 여 Azure AD를 클레임 공급자로 정의할 수 있습니다 `<ClaimsProvider>` 정책 hello 확장 파일에 있는 노드:

1. 작업 디렉터리부터 hello 확장 파일 (TrustFrameworkExtensions.xml)를 엽니다.
1. Hello `<ClaimsProviders>` 섹션. 존재 하지 않는 경우 hello 루트 노드에 추가 합니다.
1. 다음과 같이 새로운 `<ClaimsProvider>` 노드를 추가합니다.

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
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

1. Hello에서 `<ClaimsProvider>` 노드를 업데이트 hello 값에 대 한 `<Domain>` tooa 고유 값 toodistinguish 사용된 될 수 있는 기타 id 공급자에서 합니다.
1. Hello에서 `<ClaimsProvider>` 노드를 업데이트 hello 값에 대 한 `<DisplayName>` tooa 이름을 hello에 대 한 클레임 공급자입니다. 이 값은 현재 사용되지 않습니다.

### <a name="update-hello-technical-profile"></a>Hello 기술 프로필 업데이트

tooget hello Azure AD 끝점에서 토큰을 Azure AD와 Azure AD B2C toocommunicate를 사용 해야 함을 toodefine hello 프로토콜 필요 합니다. Hello 내부 이렇게 `<TechnicalProfile>` 요소의 `<ClaimsProvider>`합니다.
1. 업데이트의 hello hello ID `<TechnicalProfile>` 노드. 이 ID가 사용 되는 toorefer toothis hello 정책의 다른 부분과에서 기술 프로필.
1. 에 대 한 hello 시간 `<DisplayName>`합니다. 이 값은 hello 로그인 단추 로그인 화면에 표시 됩니다.
1. 에 대 한 hello 시간 `<Description>`합니다.
1. Hello OpenID Connect 프로토콜을 사용 하 여 azure AD를 구분 하므로 해당 hello 값에 대 한 `<Protocol>` 은 `"OpenIdConnect"`합니다.

Tooupdate hello 필요한 `<Metadata>` hello XML 파일 섹션에에서 특정에 대 한 tooearlier tooreflect hello 구성 설정 참조 Azure AD 테 넌 트입니다. Hello XML 파일에서 hello 메타 데이터 값을 다음과 같이 업데이트 합니다.

1. 설정 `<Item Key="METADATA">` 너무`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`여기서 `yourAzureADtenant` 은 Azure AD 테 넌 트 이름 (contoso.com).
1. 브라우저와 go toohello 열고 `METADATA` 방금 업데이트 하는 URL입니다.
1. Hello 브라우저에서 hello 'issuer' 개체에 대 한 확인 하 고 해당 값을 복사 합니다. Hello 다음과 같이 표시 됩니다: `https://sts.windows.net/{tenantId}/`합니다.
1. 에 대 한 hello 값을 붙여 `<Item Key="ProviderName">` hello XML 파일에 있습니다.
1. 설정 `<Item Key="client_id">` hello 응용 프로그램 등록 시와에서 toohello 응용 프로그램 ID입니다.
1. 설정 `<Item Key="IdTokenAudience">` hello 응용 프로그램 등록 시와에서 toohello 응용 프로그램 ID입니다.
1. 되도록 `<Item Key="response_types">` 너무 설정`id_token`합니다.
1. 되도록 `<Item Key="UsePolicyInRedirectUri">` 너무 설정`false`합니다.

또한 Azure AD B2C 테 넌 트 toohello Azure AD에에서 등록 toolink hello Azure AD 암호 해야 `<ClaimsProvider>` 정보:

* Hello에 `<CryptographicKeys>` hello 앞에 XML 파일 섹션에 대 한 hello 시간, `StorageReferenceId` toohello 참조 ID가 정의 된 hello 암호 (예를 들어 `ContosoAppSecret`).

### <a name="upload-hello-extension-file-for-verification"></a>확인에 대 한 hello 확장 파일 업로드

지금까지 구성한 정책을 Azure AD B2C 알 수 있도록 방법을 Azure AD 디렉터리와 toocommunicate 합니다. 없다는 문제 지금까지 사용자 정책 정당한 tooconfirm의 hello 확장 파일을 업로드 하십시오. toodo 하므로:

1. 열기 hello **모든 정책** 블레이드 Azure AD B2C 테 넌 트에 있습니다.
1. Hello 확인 **있으면 hello 정책 덮어쓰기** 상자입니다.
1. Hello 확장 파일 (TrustFrameworkExtensions.xml)를 업로드 하 고 hello 유효성 검사 실패 하지 않습니다.

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>Hello Azure AD 클레임 공급자의 tooa 사용자 여행 등록

사용자 친구의 tooadd hello Azure AD identity provider tooone를 해야 합니다. 이 시점에서 hello id 공급자 설정 되어 있지만 hello 로그-up/로그인 화면 중에서 사용할 수 없는 합니다. toomake 사용할 수 있는 것 기존 템플릿 사용자 여행 중복 만들어져 hello Azure AD id 공급자를 포함 되도록 한 다음 수정 합니다.

1. Hello 정책 (예를 들어 TrustFrameworkBase.xml)의 기본 파일을 엽니다.
1. Hello `<UserJourneys>` 전체 요소와 복사 hello `<UserJourney>` 포함 된 노드 `Id="SignUpOrSignIn"`합니다.
1. Hello 확장 파일 (예를 들어 TrustFrameworkExtensions.xml)를 열고 hello `<UserJourneys>` 요소입니다. 존재 하지 않으면 hello 요소 하나를 추가 합니다.
1. 전체 붙여넣기 hello `<UserJourney>` hello의 자식으로 복사한 노드 `<UserJourneys>` 요소입니다.
1. 새 사용자의 hello 여행의 hello ID 이름 바꾸기 (으로 이름 바꾸기 예를 들어 `SignUpOrSignUsingContoso`).

### <a name="display-hello-button"></a>디스플레이 hello "button"

hello `<ClaimsProviderSelection>` 요소 로그-up/로그인 화면에 유사한 tooan identity provider 단추입니다. 추가 하는 경우는 `<ClaimsProviderSelection>` Azure AD에 대 한 요소, 사용자 hello 페이지에 처음 삽입 새 단추 표시 합니다. tooadd이이 요소:

1. Hello `<OrchestrationStep>` 포함 된 노드 `Order="1"` 방금 만든 hello 사용자 여정에서.
1. Hello 다음을 추가 합니다.

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. 설정 `TargetClaimsExchangeId` tooan 적절 한 값입니다. 다음과 같은 hello 권장 다른 사용자와 규칙:  *\[ClaimProviderName\]Exchange*합니다.

### <a name="link-hello-button-tooan-action"></a>링크 hello 단추 tooan 동작

Toolink 필요한 위치에 있는 단추를가지고 그 tooan 동작 합니다. hello 동작이 경우 Azure AD tooreceive와 Azure AD B2C toocommunicate에 대 한 토큰입니다. Azure AD 클레임 공급자에 대 한 hello 기술 프로필을 연결 하 여 hello 단추 tooan 동작을 연결할:

1. Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.
1. Hello 다음을 추가 합니다.

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. 업데이트 `Id` 의과 같은 값인 toohello `TargetClaimsExchangeId` hello 섹션 앞에 있습니다.
1. 업데이트 `TechnicalProfileReferenceId` toohello ID의 기술 hello 프로필 앞에서 만든 (ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Hello 업데이트 된 확장 파일 업로드

Hello 확장 파일을 수정 하 고 수행 됩니다. 저장합니다. 그런 다음 hello 파일을 업로드 하 고 성공 하는 모든 유효성 검사를 확인 합니다.

### <a name="update-hello-rp-file"></a>Hello RP 파일 업데이트

이제 tooupdate hello 신뢰 당사자 (RP)에 파일이 필요 방금 만든 hello 사용자 작업을 시작 합니다.

1. 작업 디렉터리에 SignUpOrSignIn.xml의 복사본을 만들고 이름을 바꿉니다 (예를 들어 이름을 tooSignUpOrSignInWithAAD.xml).
1. 열기 hello 새 파일 및 업데이트 hello `PolicyId` 특성 `<TrustFrameworkPolicy>` 고유 값 (예를 들어 SignUpOrSignInWithAAD)으로 합니다. <br> 이 정책 hello 이름 됩니다 (예를 들어 B2C\_1A\_SignUpOrSignInWithAAD).
1. Hello 수정 `ReferenceId` 특성 `<DefaultUserJourney>` toomatch hello ID (SignUpOrSignUsingContoso) 하 여 만든 hello 새 사용자 작업입니다.
1. 변경 내용을 저장 하 고 hello 파일을 업로드 합니다.

## <a name="troubleshooting"></a>문제 해결

해당 블레이드를 열고 클릭 하 여 방금 업로드 hello 사용자 지정 정책을 테스트 **지금 실행**합니다. toodiagnose 문제에 대해 알아보세요 [문제 해결](active-directory-b2c-troubleshoot-custom.md)합니다.

## <a name="next-steps"></a>다음 단계

피드백을 너무 제공[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)합니다.
