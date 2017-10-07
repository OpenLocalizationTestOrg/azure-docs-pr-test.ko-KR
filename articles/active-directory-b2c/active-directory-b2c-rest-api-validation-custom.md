---
title: "Azure Active Directory B2C: REST API 클레임 교환을 유효성 검사로 통합 | Microsoft Docs"
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
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 사용자 입력에 대한 유효성 검사로 통합

Identity 경험 프레임 워크 (IEF) Azure Active Directory B2C 기반이 되는 hello (Azure AD B2C) hello identity 개발자 toointegrate 사용자 여정에서 RESTful API와의 상호 작용을 수 있습니다.  

이 연습의 hello 끝 수 toocreate RESTful 서비스와 상호 작용 하는 Azure AD B2C 사용자 때 고려해볼 수 있습니다.

hello IEF 데이터를 보내고 클레임의 클레임에 있는 데이터를 받습니다. hello API와 상호 작용을 hello:

- API와 상호 작용을 오케스트레이션 단계 내부에서 발생하는 REST API 클레임 교환 또는 유효성 검사 프로필로 설계할 수 있습니다.
- 일반적으로 hello 사용자의 입력을 확인합니다. Hello 사용자 로부터 hello 값이 거부 되 면 tooenter hello 기회 tooreturn 오류 메시지를 사용 하 여 유효한 값 hello 사용자 다시 시도할 수 있습니다.

또한 오케스트레이션 단계로 hello 상호 작용을 디자인할 수 있습니다. 자세한 내용은 [연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 오케스트레이션 단계로 통합](active-directory-b2c-rest-api-step-custom.md)을 참조하세요.

예: hello 유효성 검사 프로필 hello 프로필 편집 사용자 여행 ProfileEdit.xml hello 스타터 팩 파일에 사용 합니다.

Hello hello 프로필에는 사용자가 편집에 속하지 않는 한 제외 목록을 제공 해당 hello 이름을 확인할 수 있습니다.

## <a name="prerequisites"></a>필수 조건

- Azure AD B2C 테 넌 트 구성 toocomplete 로그-up/로그인에 설명 된 대로 로컬 계정 [시작](active-directory-b2c-get-started-custom.md)합니다.
- 사용 REST API 끝점 toointeract 합니다. 이 연습에서는 REST API 서비스를 사용하여 [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/)라는 데모 사이트를 설정했습니다.

## <a name="step-1-prepare-hello-rest-api-function"></a>1 단계: 준비 hello REST API 함수

> [!NOTE]
> REST API 함수는 설치 방법은이 문서의 hello 다루지 않습니다. [Azure 기능](https://docs.microsoft.com/azure/azure-functions/functions-reference) 뛰어난 toolkit hello 클라우드에서 toocreate RESTful 서비스를 제공 합니다.

`playerTag`로 예상하는 클레임을 받는 Azure 함수를 만들었습니다. hello 함수는이 클레임의 존재 여부를 확인 합니다. Hello 완전 한 Azure 함수 코드에 액세스할 수 있습니다 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)합니다.

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

hello IEF hello에서는 `userMessage` 클레임 해당 hello Azure 함수를 반환 합니다. 이 클레임 409 충돌 상태 앞 예제는 hello에 반환 될 때와 같은 hello 유효성 검사가 실패 하면 문자열 toohello 사용자로 표시 됩니다.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>2 단계: TrustFrameworkExtensions.xml 파일에서 기술 프로필로 hello RESTful API 클레임 exchange 구성

기술 프로필은 RESTful 서비스 hello로 원하는 hello 교환의 hello 전체 구성. Hello TrustFrameworkExtensions.xml 파일을 열고 다음 XML 조각 hello 내 hello 추가 `<ClaimsProviders>` 요소입니다.

> [!NOTE]
> 다음과 같은 XML을 RESTful 공급자 hello에 `Version=1.0.0.0` hello 프로토콜 설명은 다음과 같습니다. 이 hello 외부 서비스와 상호 작용 하는 hello 함수도 간주 합니다. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

hello `InputClaims` 요소 hello IEF toohello REST 서비스에서에서 전송 될 hello 클레임을 정의 합니다. 이 예제에서는 hello 클레임의 내용을 hello `givenName` toohello REST 서비스를 받게 될 `playerTag`합니다. 이 예제에서는 hello IEF에 필요 하지 않으면 다시 클레임입니다. 대신, 응답을 수신 하는 hello 상태 코드에 따라 작업을 실행 하 고 hello REST 서비스에 대 한 대기 합니다.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>3 단계: toovalidate hello 사용자 입력을 원하는 자체 어설션된 기술 프로필에 hello RESTful 서비스 클레임 교환이 포함

사용자와 상호 작용 hello hello hello 유효성 검사 단계의 가장 일반적인 용도가입니다. 여기서 hello 사용자는 입력 예상된 tooprovide 모든 상호 작용은 *기술 프로필 자체 어설션된*합니다. 예를 들어 hello 유효성 검사 toohello 자체 Asserted ProfileUpdate 기술 프로필을 추가 합니다. 이 신뢰 당사자 (RP) 정책 파일 hello hello 기술 프로필 `Profile Edit` 사용 합니다.

tooadd hello 클레임 exchange toohello 자체 기술 프로필 설정 되었습니다.

1. 파일을 열고 hello TrustFrameworkBase.xml을 검색할 `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`합니다.
2. 이 기술 프로필의 hello 구성을 검토 합니다. 클레임 (입력된 클레임) hello 사용자의 요청 수 및 hello 자체 어설션된 공급자 (출력 클레임 포함)에서 다시 예상할 수 있는 클레임으로 hello 사용자와 hello exchange가 정의 하는 방법을 확인 합니다.
3. `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`를 검색하고 이 프로필이 `<UserJourney Id="ProfileEdit">`의 6 오케스트레이션 단계로 호출되었는지 확인합니다.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>4 단계: 업로드 하 고 hello 프로필 편집 RP 정책 파일을 테스트

1. Hello 새 버전의 hello TrustFrameworkExtensions.xml 파일을 업로드 합니다.
2. 사용 하 여 **지금 실행** tootest hello 프로필 RP 정책 파일을 편집 합니다.
3. Hello에 hello 기존 이름 (예를 들어 mcvinny) 중 하나를 제공 하 여 hello 유효성 검사 테스트 **지정 된 이름** 필드입니다. 모든 설정이 올바른지, 알리는 hello 사용자 hello 플레이어 태그가 이미 사용 될 메시지를 받게 됩니다.

## <a name="next-steps"></a>다음 단계

[Hello 프로필 편집 및 사용자 등록 toogather 추가 정보에서 사용자 수정](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 오케스트레이션 단계로 통합](active-directory-b2c-rest-api-step-custom.md)
