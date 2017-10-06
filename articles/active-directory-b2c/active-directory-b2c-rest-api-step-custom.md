---
title: "Azure Active Directory B2C: REST API 클레임 교환을 오케스트레이션 단계로 통합 | Microsoft Docs"
description: "API와 통합하는 Azure Active Directory B2C 사용자 지정 정책에 대한 항목입니다."
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
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 오케스트레이션 단계로 통합

Identity 경험 프레임 워크 (IEF) Azure Active Directory B2C 기반이 되는 hello (Azure AD B2C) hello identity 개발자 toointegrate 사용자 여정에서 RESTful API와의 상호 작용을 수 있습니다.  

이 연습의 hello 끝 수 toocreate RESTful 서비스와 상호 작용 하는 Azure AD B2C 사용자 때 고려해볼 수 있습니다.

hello IEF 데이터를 보내고 클레임의 클레임에 있는 데이터를 받습니다. REST API 클레임 exchange hello:

- 오케스트레이션 단계로 설계할 수 있습니다.
- 외부 동작을 트리거할 수 있습니다. 예를 들어 외부 데이터베이스에 이벤트를 기록할 수 있습니다.
- 사용 되는 toofetch 값 되어 hello 사용자 데이터베이스에 저장 합니다.

Hello 받은 클레임을 사용할 수 있습니다 실행 이후 toochange hello 흐름입니다.

또한 유효성 검사 프로필 hello 상호 작용을 디자인할 수 있습니다. 자세한 내용은 [연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 사용자 입력에 대한 유효성 검사로 통합](active-directory-b2c-rest-api-validation-custom.md)을 참조하세요.

hello 시나리오는 사용자 프로필 편집을 수행할 때 한다고 합니다.

1. 외부 시스템의 hello 사용자를 조회 합니다.
2. 해당 사용자가 등록 되어 hello 도시를 가져옵니다.
3. 해당 특성 toohello 응용 프로그램을 클레임으로 반환 합니다.

## <a name="prerequisites"></a>필수 조건

- Azure AD B2C 테 넌 트 구성 toocomplete 로그-up/로그인에 설명 된 대로 로컬 계정 [시작](active-directory-b2c-get-started-custom.md)합니다.
- 사용 REST API 끝점 toointeract 합니다. 이 연습에서는 간단한 웹후크 Azure 함수 앱을 예제로 사용합니다.
- *권장*: 전체 hello [REST API 클레임 유효성 검사 단계로 exchange 연습](active-directory-b2c-rest-api-validation-custom.md)합니다.

## <a name="step-1-prepare-hello-rest-api-function"></a>1 단계: 준비 hello REST API 함수

> [!NOTE]
> REST API 함수는 설치 방법은이 문서의 hello 다루지 않습니다. [Azure 기능](https://docs.microsoft.com/azure/azure-functions/functions-reference) 뛰어난 toolkit hello 클라우드에서 toocreate RESTful 서비스를 제공 합니다.

호출 하는 클레임을 수신 하는 Azure 함수까지 설정한 `email`, 다음 반환 hello 클레임 및 `city` 값이 할당 된 hello `Redmond`합니다. Azure 함수 hello 샘플 켜져 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)합니다.

hello `userMessage` hello Azure 함수가 반환 하는 클레임은이 컨텍스트에서 선택 사항이 며 hello IEF을 무시 합니다. 사용할 수 있습니다 잠재적으로 메시지 toohello 응용 프로그램을 전달 하 고 뒤 toohello 사용자에서 설명 합니다.

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Azure 함수 앱 쉽게 tooget hello 함수 URL을 hello 특정 함수의 hello 식별자가 포함 되어 있습니다. 이 경우에 hello URL: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw== 합니다. 테스트 용도로 사용할 수 있습니다.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>2 단계: TrustFrameworExtensions.xml 파일에서 기술 프로필로 hello RESTful API 클레임 exchange 구성

기술 프로필은 RESTful 서비스 hello로 원하는 hello 교환의 hello 전체 구성. Hello TrustFrameworkExtensions.xml 파일을 열고 다음 XML 조각 hello 내 hello 추가 `<ClaimsProvider>` 요소입니다.

> [!NOTE]
> 다음과 같은 XML을 RESTful 공급자 hello에 `Version=1.0.0.0` hello 프로토콜 설명은 다음과 같습니다. 이 hello 외부 서비스와 상호 작용 하는 hello 함수도 간주 합니다. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

hello `<InputClaims>` 요소 hello IEF toohello REST 서비스에서에서 전송 될 hello 클레임을 정의 합니다. 이 예제에서는 hello 클레임의 내용을 hello `givenName` toohello REST 서비스 hello 클레임으로 보낼 `email`합니다.  

hello `<OutputClaims>` 요소 IEF hello REST 서비스에서 예상 되는 해당 hello hello 클레임을 정의 합니다. 받은 클레임은, hello 수에 관계 없이 hello IEF 여기에서 사용할 항목만 식별 합니다. 이 예제에서는 클레임으로 받은 `city` 매핑된 tooan IEF 클레임 이름은 `city`합니다.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>3 단계: 추가 hello 새 클레임 `city` TrustFrameworkExtensions.xml 파일의 toohello 스키마

hello 클레임 `city` 아직 정의 되지 않은 곳이 스키마에 있습니다. 따라서 hello 요소 안에 정의 추가 `<BuildingBlocks>`합니다. Hello 파일 시작 부분의 hello TrustFrameworkExtensions.xml이이 요소를 찾을 수 있습니다.

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>4 단계: TrustFrameworkExtensions.xml 사용자 프로필 편집 사용자 여정에서 오케스트레이션 단계로 hello REST 서비스 클레임 교환이 포함

단계 추가 toohello 프로필 편집 사용자 여행, hello 사용자 후에 (오케스트레이션 1-4 단계에서 다음과 같은 XML hello)를 인증 하 고 hello 사용자가 업데이트 하는 hello 프로필 정보 (5 단계)를 제공 합니다.

> [!NOTE]
> 오케스트레이션 단계로 hello REST API 호출에 사용 될 수 있는 많은 사용 사례 있습니다. 오케스트레이션 단계로,이 클래스는 사용자 처음 등록 같은 작업을 성공적으로 완료 된 후 업데이트 tooan 외부 시스템으로 사용할 수 있습니다 또는 프로필로 동기화 tookeep 정보를 업데이트 합니다. 이 경우 hello 프로필 편집 후 toohello 응용 프로그램을 제공 하는 사용 되는 tooaugment hello 정보입니다.

Hello 내 hello TrustFrameworkBase.xml 파일 tooyour TrustFrameworkExtensions.xml 파일에서 사용자의 여행 XML 코드를 편집 하는 hello 프로필 복사 `<UserJourneys>` 요소입니다. 6 단계에서 수정 hello를 확인 합니다.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Hello 순서 버전와 일치 하지 않으면 경우 hello 하기 전에 hello 단계로 hello 코드를 삽입 하는 있는지 확인 `ClaimsExchange` 형식 `SendClaims`합니다.

hello hello 사용자 작업에 대 한 최종 XML 다음과 같이 표시 됩니다.

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>5 단계: 추가 hello 클레임 `city` hello 클레임 tooyour 응용 프로그램 보내도록 tooyour 신뢰 당사자 정책 파일

ProfileEdit.xml 신뢰 당사자 (RP) 파일을 편집 하 고 hello를 수정할 `<TechnicalProfile Id="PolicyProfile">` 요소 tooadd hello 다음: `<OutputClaim ClaimTypeReferenceId="city" />`합니다.

Hello 새 클레임을 추가한 후 hello 기술 프로필은 다음과 같습니다.

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>6단계 - 변경 내용 업로드 및 테스트

기존 버전의 hello 정책 hello를 덮어씁니다.

1.  (선택 사항:) 계속 진행 하기 전에 hello 기존 버전 (다운로드) 하 여 확장 파일의 저장 합니다. tookeep hello 초기 복잡성 낮은 hello 확장 파일의 여러 버전을 업로드 하지 않는 두는 것이 좋습니다.
2.  (선택 사항:) Hello hello 정책 파일 편집에 대 한 hello 정책 ID의 새 버전을 변경 하 여 이름 바꾸기 `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`합니다.
3.  Hello 확장 파일을 업로드 합니다.
4.  Hello 정책 편집 RP 파일을 업로드 합니다.
5.  사용 하 여 **지금 실행** tootest hello 정책입니다. IEF hello 검토 hello 토큰 toohello 응용 프로그램을 반환 합니다.

모든 설정이 올바른지, hello 토큰 hello 새 클레임을 포함 됩니다 `city`, hello 값을 가진 `Redmond`합니다.

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>다음 단계

[유효성 검증 단계로 REST API 사용](active-directory-b2c-rest-api-validation-custom.md)

[Hello 프로필 편집 toogather 추가 정보를 사용자가 수정 합니다.](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
