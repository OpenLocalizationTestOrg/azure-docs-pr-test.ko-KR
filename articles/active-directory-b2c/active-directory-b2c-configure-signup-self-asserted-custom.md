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
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="ed2fc-103">Azure Active Directory B2C: tooadd 새 클레임 등록을 수정 하 고 사용자 입력을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ed2fc-104">이 문서에서 새 사용자가 제공한 항목 (클레임) tooyour signup 사용자 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="ed2fc-105">드롭다운을으로 hello 항목을 구성 하 고 필요한 경우 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="ed2fc-106">Sipi tootrigger 테스트 전달 하 여 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed2fc-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ed2fc-107">Prerequisites</span></span>

* <span data-ttu-id="ed2fc-108">Hello 문서에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="ed2fc-109">Hello 등록/signin 사용자 여행 toosignup 새로운 로컬 계정을 계속 진행 하기 전에 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="ed2fc-110">사용자로부터 초기 데이터 수집은 등록/로그인을 통해 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="ed2fc-111">프로필 편집 사용자 경험을 통해 추가 클레임을 나중에 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="ed2fc-112">Azure AD B2C를 대화형으로 hello 사용자 로부터 직접 정보 수집, 언제 든 지 hello Id 경험 프레임 워크 사용 하 여 해당 `selfasserted provider`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="ed2fc-113">hello 단계 아래에이 공급자를 사용할 때 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="ed2fc-114">Hello 클레임, 표시 이름 및 hello 사용자 입력 유형 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="ed2fc-115">해당 도시에 대 한 hello 사용자에 게 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="ed2fc-116">다음 요소 toohello hello 추가 `<ClaimsSchema>` hello TrustFrameWorkExtensions 정책 파일의 요소:</span><span class="sxs-lookup"><span data-stu-id="ed2fc-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="ed2fc-117">추가 선택 항목이 클레임 toocustomize hello 여기 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="ed2fc-118">전체 스키마에 대 한 참조 toohello **Id 경험 프레임 워크 기술 참조 가이드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="ed2fc-119">이 가이드는 hello 참조 섹션에 곧 발표 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="ed2fc-120">`<DisplayName>`사용자 용 hello를 정의 하는 문자열은 *레이블*</span><span class="sxs-lookup"><span data-stu-id="ed2fc-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="ed2fc-121">`<UserHelpText>`hello 사용자를 필요한 것을 이해 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="ed2fc-122">`<UserInputType>`가 hello 다음 네 가지 옵션 아래에 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="ed2fc-123">`RadioSingleSelectduration` - 단일 선택을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="ed2fc-124">`DropdownSingleSelect`-유효한 값만 hello 선택할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

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


* <span data-ttu-id="ed2fc-126">`CheckboxMultiSelect`하나 이상의 값 hello 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

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

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="ed2fc-128">Hello 클레임 toohello 기호 위쪽/여행 사용자 로그인 추가</span><span class="sxs-lookup"><span data-stu-id="ed2fc-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="ed2fc-129">Hello 클레임으로 추가 `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (hello TrustFrameworkBase 정책 파일에 있는).</span><span class="sxs-lookup"><span data-stu-id="ed2fc-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="ed2fc-130">Note이 TechnicalProfile SelfAssertedAttributeProvider hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

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

2. <span data-ttu-id="ed2fc-131">으로 hello 클레임 toohello AAD UserWriteUsingLogonEmail 추가 `<PersistedClaim ClaimTypeReferenceId="city" />` hello 사용자 로부터 수집한 후 toowrite hello 클레임 toohello AAD 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="ed2fc-132">하지 toopersist hello 클레임 hello 디렉터리에 나중에 사용할 선호 하는 경우이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

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

3. <span data-ttu-id="ed2fc-133">Hello 클레임 toohello TechnicalProfile 사용자로 로그인 할 때 hello 디렉터리에서 읽을 수 있는 추가 프로그램`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="ed2fc-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

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

4. <span data-ttu-id="ed2fc-134">Hello 추가 `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP 정책 파일 SignUporSignIn.xml 하므로이 클레임 사용자 성공 여행 후 hello 토큰에 toohello 응용 프로그램에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

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

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="ed2fc-135">"Run Now"를 사용 하 여 hello 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="ed2fc-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="ed2fc-136">열기 hello **Azure AD B2C 블레이드** 너무 이동**Id 경험 프레임 워크 > 사용자 지정 정책의**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="ed2fc-137">업로드 하는 hello 사용자 지정 정책을 선택 하 고 hello 클릭 **지금 실행** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="ed2fc-138">전자 메일 주소를 사용 하 여 수 toosign 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="ed2fc-139">테스트 모드에서 hello 등록 화면 비슷한 toothis 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-139">hello signup screen in test mode should look similar toothis:</span></span>

![수정된 등록 옵션의 스크린샷](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="ed2fc-141">hello 토큰 백 tooyour 응용 프로그램은 이제 포함 hello `city` 아래 표시 된 대로 클레임</span><span class="sxs-lookup"><span data-stu-id="ed2fc-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="ed2fc-142">선택 사항: 등록 경험에서 전자 메일 확인 제거</span><span class="sxs-lookup"><span data-stu-id="ed2fc-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="ed2fc-143">tooskip 전자 메일 확인 hello 정책 작성자 tooremove를 선택할 수 `PartnerClaimType="Verified.Email"`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="ed2fc-144">hello 전자 메일 주소는 필요한 되지만 유효성을 검사 하지 않으면 "Required" = true 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="ed2fc-145">이 옵션이 사용자의 사용 사례에 적합한지 신중하게 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="ed2fc-146">Hello에서 기본적으로 전자 메일 활성화가 확인 `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` hello 스타터 팩에서 hello TrustFrameworkBase 정책 파일에:</span><span class="sxs-lookup"><span data-stu-id="ed2fc-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="ed2fc-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed2fc-147">Next steps</span></span>

<span data-ttu-id="ed2fc-148">아래에 나열 된 TechnicalProfiles hello를 변경 하 여 소셜 계정 로그인에 대 한 hello 새 클레임 toohello 흐름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="ed2fc-149">로케이터 hello hello alternativeSecurityId 사용 하 여 hello 사용자 데이터를 읽을 고 사회/페더레이션 계정 로그인 toowrite에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed2fc-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
