---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 ID 공급자로 MSA(Microsoft 계정) 추가"
description: "OIDC(Microsoft OpenID 연결) 프로토콜을 사용하는 ID 공급자로 Microsoft를 사용하는 샘플"
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: 사용자 지정 정책을 사용하여 ID 공급자로 MSA(Microsoft 계정) 추가

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

이 문서에서는 어떻게 tooenable 로그인 Microsoft 계정 (MSA)에서 사용자에 대 한 hello 사용을 통해 [사용자 지정 정책을](active-directory-b2c-overview-custom.md)합니다.

## <a name="prerequisites"></a>필수 조건
Hello에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md) 문서.

이러한 단계는 다음과 같습니다.

1.  Microsoft 계정 응용 프로그램 만들기
2.  Hello Microsoft 계정이 응용 프로그램 키 tooAzure AD B2C 추가
3.  클레임 공급자 tooa 정책 추가
4.  Hello Microsoft 계정 클레임 공급자의 tooa 사용자 여행을 등록 하는 중
5.  테 넌 트 hello 정책 tooan Azure AD B2C 업로드 하 고 테스트

## <a name="create-a-microsoft-account-application"></a>Microsoft 계정 응용 프로그램 만들기
(Azure AD) Azure Active Directory B2C에 대 한 id 공급자로 toouse Microsoft 계정, Microsoft 계정 응용 프로그램 toocreate 필요 하 고 hello 오른쪽 매개 변수를 제공 합니다. Microsoft 계정이 있어야 합니다. 계정이 없는 경우 [https://www.live.com/](https://www.live.com/)을 방문합니다.

1.  Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) Microsoft 계정 자격 증명으로 로그인 합니다.
2.  **앱 추가**를 클릭합니다.

    ![Microsoft 계정 - 앱 추가](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  응용 프로그램에 **이름**을 제공하고 **전자 메일로 연락하고**, **시작하도록 지원 받기**의 선택을 취소하고, **만들기**를 클릭합니다.

    ![Microsoft 계정 - 응용 프로그램 등록](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  hello 값을 복사 **응용 프로그램 Id**합니다. 필요한 tooconfigure Microsoft 계정을 id 공급자로 테 넌 트에 있습니다.

    ![Microsoft 계정-응용 프로그램 Id의 hello 값 복사](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  **플랫폼 추가**를 클릭합니다.

    ![Microsoft 계정 - 플랫폼 추가](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  Hello 플랫폼 목록에서 선택 **웹**합니다.

    ![Microsoft 계정-hello 플랫폼 목록에서 선택 웹](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  입력 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **리디렉션 Uri** 필드입니다. **{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다.

    ![Microsoft 계정 - 리디렉션 URL 설정](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  클릭 **새 암호를 생성할** hello에서 **응용 프로그램 암호** 섹션. Hello 화면에 표시 되는 새 암호를 복사 합니다. 필요한 tooconfigure Microsoft 계정을 id 공급자로 테 넌 트에 있습니다. 이 암호는 중요한 보안 자격 증명입니다.

    ![Microsoft 계정-새 암호 생성](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft 계정-복사 hello에 대 한 새 암호](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  Hello 확인란의 **라이브 SDK 지원** hello에서 **고급 옵션** 섹션. **Save**를 클릭합니다.

    ![Microsoft 계정-Live SDK 지원](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>Hello Microsoft 계정이 응용 프로그램 키 tooAzure AD B2C 추가
Microsoft 계정으로 페더레이션 hello 응용 프로그램 대신 Microsoft 계정 tootrust Azure AD B2C에 대 한 클라이언트 암호에 필요 합니다. Azure AD B2C 테 넌 트에 Microsoft 계정이 응용 프로그램 secert toostore 필요합니다.   

1.  Tooyour Azure AD B2C 테 넌 트를 이동 하 고 선택 **B2C 설정** > **Id 경험 프레임 워크**
2.  선택 **정책 키** 테 넌 트에 사용할 수 있는 tooview hello 키입니다.
3.  **+추가**를 클릭합니다.
4.  **옵션**에는 **수동**을 사용합니다.
5.  **이름**에는 `MSASecret`를 사용합니다.  
    hello 접두사 `B2C_1A_` 자동으로 추가 될 수도 있습니다.
6.  Hello에 **비밀** 상자 https://apps.dev.microsoft.com에서 Microsoft 응용 프로그램 암호를 입력 합니다
7.  **키 사용**에는 **서명**을 사용합니다.
8.  **만들기**
9.  Hello 키를 만든 확인 `B2C_1A_MSASecret`합니다.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>확장 정책에서 클레임 공급자 추가
Microsoft 계정을 사용 하 여 사용자가 toosign의 하려는 경우를 클레임 공급자로 toodefine Microsoft 계정이 필요 합니다. 즉, Azure AD B2C와 통신 하는 끝점 toospecify를 해야 합니다. hello 끝점은 특정 사용자가 인증 하는 Azure AD B2C tooverify에서 사용 되는 클레임 집합을 제공 합니다.

확장 정책 파일에서 `<ClaimsProvider>` 노드를 추가하여 Microsoft 계정을 클레임 공급자로 정의합니다.

1.  작업 디렉터리부터 hello 확장명 정책 파일 (TrustFrameworkExtensions.xml)을 엽니다. XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).
2.  Hello `<ClaimsProviders>` 섹션
3.  Hello 아래 XML 조각 다음 추가 `ClaimsProviders` 요소:

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  `client_id` 값을 Microsoft 계정 응용 프로그램 클라이언트 ID로 바꿉니다.

5.  Hello 파일을 저장 합니다.

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Hello 클레임 공급자 tooSign Microsoft 계정 또는 사용자 여행 로그인 등록

이 시점에서 hello id 공급자 설정 되어 있지만 hello 로그-up/로그인 화면 중에서 사용할 수 없는 합니다. 이제 tooadd hello Microsoft 계정 id 공급자 tooyour 사용자 필요한 `SignUpOrSignIn` 사용자 여행 합니다. toomake 기존 템플릿 사용자 여행 중복 만듭니다 사용할 수 있는 것입니다.  Hello Microsoft 계정 id 공급자로 추가합니다.

> [!NOTE]
>
>Hello 이전에 복사한 경우 `<UserJourneys>` 정책 toohello 확장 프로그램 파일의 기본 파일에서 요소 `TrustFrameworkExtensions.xml`, toothis 섹션을 건너뛸 수 있습니다.

1.  Hello 정책 (예를 들어 TrustFrameworkBase.xml)의 기본 파일을 엽니다.
2.  Hello `<UserJourneys>` 의 요소와 복사 hello 전체 내용을 `<UserJourneys>` 노드.
3.  Hello 확장 파일 (예를 들어 TrustFrameworkExtensions.xml)를 열고 hello `<UserJourneys>` 요소입니다. 존재 하지 않으면 hello 요소 하나를 추가 합니다.
4.  전체 내용을 hello `<UserJournesy>` hello의 자식으로 복사한 노드 `<UserJourneys>` 요소입니다.

### <a name="display-hello-button"></a>디스플레이 hello 단추
hello `<ClaimsProviderSelections>` 요소 hello 클레임 공급자 선택 옵션 목록 및 해당 순서를 정의 합니다.  `<ClaimsProviderSelection>`요소는 로그-up/로그인 페이지에 유사한 tooan identity provider 단추입니다. 추가 하는 경우는 `<ClaimsProviderSelection>` Microsoft 계정에 대 한 요소, 사용자 hello 페이지에 처음 삽입 새 단추 표시 합니다. tooadd이이 요소:

1.  Hello `<UserJourney>` 포함 된 노드 `Id="SignUpOrSignIn"` 복사한 hello 사용자 여정에서 합니다.
2.  Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`
3.  `<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>링크 hello 단추 tooan 동작
Toolink 필요한 위치에 있는 단추를가지고 그 tooan 동작 합니다. hello 동작이 경우 Microsoft 계정 tooreceive와 Azure AD B2C toocommunicate에 대 한 토큰입니다. Microsoft 계정 클레임 공급자에 대 한 hello 기술 프로필을 연결 하 여 hello 단추 tooan 동작을 연결할:

1.  Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.
2.  `<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * Hello 확인 `Id` 의과 같은 값인 hello에 `TargetClaimsExchangeId` hello 앞 섹션에서
>   * 확인 `TechnicalProfileReferenceId` 이전 (MSA OIDC)를 만든 toohello 기술 프로필 ID가 설정 되어 있습니다.

## <a name="upload-hello-policy-tooyour-tenant"></a>Hello 정책 tooyour 테 넌 트에 업로드
1.  Hello에 [Azure 포털](https://portal.azure.com), hello를 전환 [Azure AD B2C 테 넌 트의 상황에 맞는](active-directory-b2c-navigate-to-b2c-context.md), 및 열기 hello **Azure AD B2C** 블레이드입니다.
2.  **ID 경험 프레임워크**를 선택합니다.
3.  열기 hello **모든 정책** 블레이드입니다.
4.  **정책 업로드**를 선택합니다.
5.  확인 **있으면 hello 정책 덮어쓰기** 상자입니다.
6.  **업로드** TrustFrameworkExtensions.xml hello 유효성 검사가 발생 하지 않도록 하 고

## <a name="test-hello-custom-policy-by-using-run-now"></a>지금 실행에 사용 하 여 hello 사용자 지정 정책 테스트

1.  열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.
> [!NOTE]
>
>**지금 실행** hello 테 넌 트에 응용 프로그램이 하나 이상 toobe 미리 등록 필요 합니다. toolearn tooregister 응용 프로그램을 확인 하려면 어떻게 해야 Azure AD B2C hello [시작](active-directory-b2c-get-started.md) 문서 또는 hello [응용 프로그램 등록](active-directory-b2c-app-registration.md) 문서.
2.  열기 **B2C_1A_signup_signin**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다. **지금 실행**을 선택합니다.
3.  Microsoft 계정을 사용 하 여 수 toosign 있어야 합니다.

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[선택 사항] Hello Microsoft 계정 클레임 공급자의 tooProfile 편집 사용자 여행 등록
좋습니다 tooadd hello Microsoft 계정 id 공급자도 tooyour 사용자 `ProfileEdit` 사용자 여행 합니다. toomake 마지막 두 단계 hello 반복 사용할 수 있습니다.

### <a name="display-hello-button"></a>디스플레이 hello 단추
1.  정책 (예를 들어 TrustFrameworkExtensions.xml) hello 확장 파일을 엽니다.
2.  Hello `<UserJourney>` 포함 된 노드 `Id="ProfileEdit"` 복사한 hello 사용자 여정에서 합니다.
3.  Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`
4.  `<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>링크 hello 단추 tooan 동작
1.  Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.
2.  `<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>지금 실행에 사용 하 여 hello 사용자 지정 프로필 편집 정책 테스트
1.  열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.
2.  열기 **B2C_1A_ProfileEdit**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다. **지금 실행**을 선택합니다.
3.  Microsoft 계정을 사용 하 여 수 toosign 있어야 합니다.

## <a name="download-hello-complete-policy-files"></a>Hello 완성 된 정책 파일을 다운로드
선택 사항: 권장 사용자 고유의 사용자 지정 정책 파일을 사용 하 여 이러한 샘플 파일을 사용 하는 대신 안내 사용자 지정 정책을 사용 하 여 시작 하는 hello를 완료 한 후 시나리오를 작성 합니다.  [참조할 샘플 정책 파일](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
