---
title: "Azure Active Directory B2C: 사용자의 고유한 특성 toocustom 정책을 추가 하 고 프로필 편집에 사용 하 | Microsoft Docs"
description: "확장 속성을 사용자 지정 특성을 사용 하 고 hello 사용자 인터페이스에 포함 하는 연습"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Azure Active Directory B2C: 사용자 지정 프로필 편집 정책에서 사용자 지정 특성을 만들고 사용

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

이 문서에서는 Azure AD B2C 디렉터리에 사용자 지정 특성을 만들 및 hello 프로필 편집 사용자 작업의 사용자 지정 클레임으로이 새 특성을 사용 합니다.

## <a name="prerequisites"></a>필수 조건

Hello 문서에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md)합니다.

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>사용자 지정 정책을 사용 하 여 Azure Active Directory B2C에 고객에 대 한 사용자 지정 특성 toocollect 정보를 사용 하 여
Azure Active Directory(Azure AD) B2C 디렉터리에는 지정된 이름, 성, 도시, 우편 번호, userPrincipalName의 특성 집합이 함께 제공됩니다.  Toocreate 사용자 고유의 특성 주로 해야 합니다.  예:
* 고객 지향 응용 프로그램이 있어야 toopersist "LoyaltyNumber."와 같은 특성
* ID 공급자는 "uniqueUserGUID"처럼 저장해야 하는 고유한 사용자 ID를 포함합니다.
* 사용자 지정 사용자 여행 필요 "migrationStatus."와 같은 사용자의 toopersist hello 상태

Azure AD B2C hello 각 사용자 계정에 저장 하는 특성 집합을 확장할 수 있습니다. 또한 읽고 수 hello를 사용 하 여 이러한 특성을 쓸 [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)합니다.

확장 속성 hello 디렉터리에 hello 사용자 개체의 hello 스키마를 확장합니다.  hello 용어 확장 속성, 사용자 지정 특성 및 사용자 지정 클레임 toohello hello 컨텍스트 (응용 프로그램, 개체, 정책)에 따라 달라 집니다이 문서와 hello 이름의 hello 컨텍스트에서 동일한 작업을 참조 하십시오.

확장 속성은 사용자에 대한 데이터를 포함할 수 있더라도 응용 프로그램 개체에만 등록할 수 있습니다. hello 속성은 연결 된 toohello 응용 프로그램입니다. hello 응용 프로그램 개체에는 쓰기 권한을 부여한 tooregister 확장 속성 이어야 합니다. (모든 형식 및 모든 응용 프로그램)에서 확장 속성을 100 tooany 단일 개체를 작성할 수 있습니다. 확장 속성 toohello 대상 디렉터리 유형에 추가 되 고 hello Azure AD B2C 디렉터리 테 넌 트에 즉시 액세스할 수 있게 됩니다.
Hello 응용 프로그램을 삭제 하면 모든 사용자에 대해 여기에 포함 된 데이터와 함께 해당 확장 속성 제거 됩니다. Hello에 없어지기 hello 응용 프로그램에서 확장 속성 삭제 되 면 대상 디렉터리 개체 및 hello 삭제 하는 값입니다.

확장 속성 hello 테 넌 트에 등록된 된 응용 프로그램의 hello 컨텍스트 에서만에서 존재합니다. 해당 응용 프로그램의 개체 id hello TechnicalProfile 사용 하는 hello에 포함 되어야 합니다.

>[!NOTE]
>hello Azure AD B2C 디렉터리 라는 웹 앱을 일반적으로 포함 `b2c-extensions-app`합니다.  이 응용 프로그램은 주로 hello Azure 포털을 통해 만든 hello 사용자 지정 클레임에 대 한 hello b2c에 대 한 기본 제공 정책에서 사용 됩니다.  고급 사용자에 게이 응용 프로그램 tooregister 확장을 사용 하 여 b2c 사용자 지정 정책에 대 한 것이 좋습니다.  이 대 한 지침은이 문서의 다음 단계 섹션 hello에 포함 됩니다.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>새 응용 프로그램 toostore hello 확장 속성 만들기

1. 검색 세션을 열고 toohello 이동 [Azure 포털](https://portal.azure.com) hello tooconfigure B2C 디렉터리의 관리자 자격 증명으로 로그인 합니다.
1. 클릭 **Azure Active Directory** hello 왼쪽된 탐색 메뉴에 있습니다. 선택 하 여 더 명의 toofind 할 수 있습니다 > 합니다.
1. **앱 등록**을 선택하고 **새 응용 프로그램 등록**을 클릭합니다.
1. Hello 다음 권장 항목을 제공 합니다.
  * Hello 웹 응용 프로그램에 대 한 이름을 지정: **WebApp-GraphAPI-DirectoryExtensions**
  * 응용 프로그램 유형: 웹앱/API
  * 로그온 URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions
1. **만들기를 선택합니다. Hello에 성공적으로 완료 표시 **알림**
1. 새로 만든 hello 웹 응용 프로그램 선택: **WebApp-GraphAPI-DirectoryExtensions**
1. **필요한 권한** 설정을 선택합니다.
1. **Windows Active Directory** API를 선택합니다.
1. **디렉터리 데이터 읽기 및 쓰기** 응용 프로그램 권한을 확인 표시하고 **저장**을 선택합니다.
1. **사용 권한 부여**를 선택하고 **예**를 확인합니다.
1. Tooyour 클립보드를 복사 하 고 hello 식별자 WebApp-GraphAPI-DirectoryExtensions에서 다음 저장 > 설정 > 속성 >
*  **응용 프로그램 ID** - 예: `103ee0e6-f92d-4183-b576-8c3739027780`
* **개체 ID** - 예: `80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>사용자 지정 정책 tooadd hello ApplicationObjectId 수정

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
>hello <TechnicalProfile Id="AAD-Common"> 해당 요소에 포함 되어 hello 요소를 사용 하 여 모든 hello Azure Active Directory TechnicalProfiles에서에서 다시 사용 하기 때문에 참조 된 tooas "공용" 됩니다.`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Hello TechnicalProfile hello 첫 번째 시간 toohello 새로 만든 확장 속성을 기록 하는 경우 일회성 오류가 발생할 수 있습니다.  hello 확장 속성은 만들어집니다 hello 처음으로 사용 됩니다.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>Hello 새 확장 속성을 사용 하 여 사용자 지정 특성을 사용자 여행 /


1. 정책에 설명 하는 신뢰 Party(RP) 파일 열기 hello 사용자 작업을 편집 합니다.  시작 하는 경우 프로그램 이미 구성 된 버전의 hello RP PolicyEdit hello hello Azure 포털에서에서 Azure B2C 사용자 지정 정책 섹션에서 직접 파일 권장 toodownload 수 있습니다.  또는 저장소 폴더에서 XML 파일을 엽니다.
2. 사용자 지정 클레임 `loyaltyId`를 추가합니다.  Hello 사용자 지정을 포함 하 여 hello에 클레임 `<RelyingParty>` 요소, 매개 변수 toohello UserJourney TechnicalProfiles 변수로 전달 되 고 hello 응용 프로그램에 대 한 hello 토큰에 포함 합니다.
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. 클레임 정의 toohello 확장명 정책 파일을 추가 `TrustFrameworkExtensions.xml` hello 내 `<ClaimsSchema>` 요소와 같이 합니다.
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. Hello 추가 정의 toohello 기본 정책 파일을 클레임 동일 `TrustFrameworkBase.xml`합니다.  
>하지만 추가 `ClaimType` hello 자료 및 hello 확장 파일 정의 일반적으로 필요 hello 정책 유효성 검사기는 hello 업로드를 거부 hello 다음 단계 hello extension_loyaltyId tooTechnicalProfiles hello 기본 파일에서을 추가 하는 이후 hello 없이 기본 파일입니다.
>Hello TrustFrameworkBase.xml 파일에서 "ProfileEdit" 라는 hello 사용자 작업의 유용한 tootrace hello 실행 수 있습니다.  Hello 동일 하면 편집기의 이름을 지정 하 고 5 단계 오케스트레이션 호출 hello TechnicalProfileReferenceID 있는지 관찰의 hello 사용자 작업에 대 한 검색 "SelfAsserted ProfileUpdate" = 합니다.  검색 하 고 hello 흐름에 따라 직접이 TechnicalProfile toofamiliarize를 검사 합니다.
5. Hello TechnicalProfile "SelfAsserted ProfileUpdate"의 입력 및 출력 클레임으로 loyaltyId 추가
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. Hello hello 디렉터리의 현재 사용자에 대 한 hello 확장 속성에 hello 클레임의 TechnicalProfile "AAD UserWriteProfileUsingObjectId" toopersist hello 값에 클레임을 추가 합니다.
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. 사용자가 로그인 할 때마다 TechnicalProfile "AAD UserReadUsingObjectId" tooread hello hello 확장 특성 값에 클레임을 추가 합니다. 지금까지 hello TechnicalProfiles 로컬 계정의 hello 흐름에서 변경 되었습니다.  사회/페더레이션 계정의 hello 흐름에서 hello 새 특성을 사용할 경우 다른 집합이 TechnicalProfiles toobe 변경 해야 합니다. 다음 단계를 참조하세요.

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
>hello IncludeTechnicalProfile 요소 AAD 공통 toothis TechnicalProfile의 모든 hello 요소를 추가합니다.

## <a name="test-hello-custom-policy-using-run-now"></a>"Run Now"를 사용 하 여 hello 사용자 지정 정책 테스트
1. 열기 hello **Azure AD B2C 블레이드** 너무 이동**Id 경험 프레임 워크 > 사용자 지정 정책의**합니다.
1. 업로드 하는 hello 사용자 지정 정책을 선택 하 고 hello 클릭 **지금 실행** 단추입니다.
1. 전자 메일 주소를 사용 하 여 수 toosign 있어야 합니다.

hello id 토큰 tooyour 응용 프로그램을 사용자 지정 클레임 extension_loyaltyId 앞으로 hello 새 확장 속성에 다시 보냈습니다. 예제를 참조하세요.

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a>다음 단계

TechnicalProfiles 나열 된 hello를 변경 하 여 소셜 계정 로그인에 대 한 hello 새 클레임 toohello 흐름을 추가 합니다. 이러한 두 TechnicalProfiles 사회/페더레이션 계정 로그인 toowrite 사용 하 고 hello 사용자 개체의 로케이터 hello hello alternativeSecurityId 사용 하 여 hello 사용자 데이터를 읽이 됩니다.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

기본 및 사용자 지정 정책 간에 동일한 확장 특성 hello를 사용 하 여 합니다.
Hello를 사용 하 여 이러한 특성은 등록 hello 포털 경험을 통해 확장 특성 (즉, 사용자 지정 특성의 경우)를 추가 하면 * * b2c-확장-app 모든 b2c 테 넌 트에 존재 합니다.  toouse 사용자 지정 정책에서 이러한 확장 특성:
1. B2c 테 넌 트에 portal.azure.com 내에서 이동 너무**Azure Active Directory** 선택 **앱 등록**
2. **b2c-확장-앱**을 찾고 선택
3. 'Essentials' 레코드 hello에서 **응용 프로그램 ID** 및 hello **개체 ID**
4. 다음과 같이 AAD 공용 기술 프로필 메타데이터에 포함:

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

hello 포털 환경과 tookeep 일관성 hello 포털 UI를 사용 하 여 이러한 특성을 만들 *전에* 지정 정책에서 사용 합니다.  를 만들 때 특성 "ActivationStatus" hello 포털에서 다음과 같이 tooit을 참조 해야 합니다.

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>참조

* A **기술 프로필 (TP)** 요소 형식인로 간주 될 수 있는 한 *함수* 끝점의 이름, 해당 메타 데이터, 해당 프로토콜을 정의 하 고 세부 정보 hello Identity hello 클레임 교환을 경험 프레임 워크를 수행 해야 합니다.  때이 *함수* 다른 TechnicalProfile, InputClaims 및 OutputClaims은 hello 호출자가 매개 변수로 제공 됩니다 hello 또는 오케스트레이션 단계에서 호출 됩니다.


* 확장 속성에 대해 전체 처리를 위해 hello 문서 참조 [디렉터리 스키마 확장 | GRAPH API 개념](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Hello 규칙을 사용 하 여 Graph API에 대 한 확장 특성 이름은 `extension_ApplicationObjectID_attributename`합니다. 따라서 XML hello에 ApplicationObjectId hello 생략 extension_attributename로 tooextensions 특성을 참조 하는 사용자 지정 정책
