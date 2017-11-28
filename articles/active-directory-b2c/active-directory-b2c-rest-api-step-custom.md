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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="dd9d4-103">연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 오케스트레이션 단계로 통합</span><span class="sxs-lookup"><span data-stu-id="dd9d4-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="dd9d4-104">Identity 경험 프레임 워크 (IEF) Azure Active Directory B2C 기반이 되는 hello (Azure AD B2C) hello identity 개발자 toointegrate 사용자 여정에서 RESTful API와의 상호 작용을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="dd9d4-105">이 연습의 hello 끝 수 toocreate RESTful 서비스와 상호 작용 하는 Azure AD B2C 사용자 때 고려해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="dd9d4-106">hello IEF 데이터를 보내고 클레임의 클레임에 있는 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="dd9d4-107">REST API 클레임 exchange hello:</span><span class="sxs-lookup"><span data-stu-id="dd9d4-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="dd9d4-108">오케스트레이션 단계로 설계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="dd9d4-109">외부 동작을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-109">Can trigger an external action.</span></span> <span data-ttu-id="dd9d4-110">예를 들어 외부 데이터베이스에 이벤트를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="dd9d4-111">사용 되는 toofetch 값 되어 hello 사용자 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="dd9d4-112">Hello 받은 클레임을 사용할 수 있습니다 실행 이후 toochange hello 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="dd9d4-113">또한 유효성 검사 프로필 hello 상호 작용을 디자인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="dd9d4-114">자세한 내용은 [연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 사용자 입력에 대한 유효성 검사로 통합](active-directory-b2c-rest-api-validation-custom.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="dd9d4-115">hello 시나리오는 사용자 프로필 편집을 수행할 때 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="dd9d4-116">외부 시스템의 hello 사용자를 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="dd9d4-117">해당 사용자가 등록 되어 hello 도시를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="dd9d4-118">해당 특성 toohello 응용 프로그램을 클레임으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd9d4-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dd9d4-119">Prerequisites</span></span>

- <span data-ttu-id="dd9d4-120">Azure AD B2C 테 넌 트 구성 toocomplete 로그-up/로그인에 설명 된 대로 로컬 계정 [시작](active-directory-b2c-get-started-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="dd9d4-121">사용 REST API 끝점 toointeract 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="dd9d4-122">이 연습에서는 간단한 웹후크 Azure 함수 앱을 예제로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="dd9d4-123">*권장*: 전체 hello [REST API 클레임 유효성 검사 단계로 exchange 연습](active-directory-b2c-rest-api-validation-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="dd9d4-124">1 단계: 준비 hello REST API 함수</span><span class="sxs-lookup"><span data-stu-id="dd9d4-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="dd9d4-125">REST API 함수는 설치 방법은이 문서의 hello 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="dd9d4-126">[Azure 기능](https://docs.microsoft.com/azure/azure-functions/functions-reference) 뛰어난 toolkit hello 클라우드에서 toocreate RESTful 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="dd9d4-127">호출 하는 클레임을 수신 하는 Azure 함수까지 설정한 `email`, 다음 반환 hello 클레임 및 `city` 값이 할당 된 hello `Redmond`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="dd9d4-128">Azure 함수 hello 샘플 켜져 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="dd9d4-129">hello `userMessage` hello Azure 함수가 반환 하는 클레임은이 컨텍스트에서 선택 사항이 며 hello IEF을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="dd9d4-130">사용할 수 있습니다 잠재적으로 메시지 toohello 응용 프로그램을 전달 하 고 뒤 toohello 사용자에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

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

<span data-ttu-id="dd9d4-131">Azure 함수 앱 쉽게 tooget hello 함수 URL을 hello 특정 함수의 hello 식별자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="dd9d4-132">이 경우에 hello URL: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw== 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="dd9d4-133">테스트 용도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="dd9d4-134">2 단계: TrustFrameworExtensions.xml 파일에서 기술 프로필로 hello RESTful API 클레임 exchange 구성</span><span class="sxs-lookup"><span data-stu-id="dd9d4-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="dd9d4-135">기술 프로필은 RESTful 서비스 hello로 원하는 hello 교환의 hello 전체 구성.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="dd9d4-136">Hello TrustFrameworkExtensions.xml 파일을 열고 다음 XML 조각 hello 내 hello 추가 `<ClaimsProvider>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="dd9d4-137">다음과 같은 XML을 RESTful 공급자 hello에 `Version=1.0.0.0` hello 프로토콜 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="dd9d4-138">이 hello 외부 서비스와 상호 작용 하는 hello 함수도 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="dd9d4-139">hello `<InputClaims>` 요소 hello IEF toohello REST 서비스에서에서 전송 될 hello 클레임을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="dd9d4-140">이 예제에서는 hello 클레임의 내용을 hello `givenName` toohello REST 서비스 hello 클레임으로 보낼 `email`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="dd9d4-141">hello `<OutputClaims>` 요소 IEF hello REST 서비스에서 예상 되는 해당 hello hello 클레임을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="dd9d4-142">받은 클레임은, hello 수에 관계 없이 hello IEF 여기에서 사용할 항목만 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="dd9d4-143">이 예제에서는 클레임으로 받은 `city` 매핑된 tooan IEF 클레임 이름은 `city`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="dd9d4-144">3 단계: 추가 hello 새 클레임 `city` TrustFrameworkExtensions.xml 파일의 toohello 스키마</span><span class="sxs-lookup"><span data-stu-id="dd9d4-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="dd9d4-145">hello 클레임 `city` 아직 정의 되지 않은 곳이 스키마에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="dd9d4-146">따라서 hello 요소 안에 정의 추가 `<BuildingBlocks>`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="dd9d4-147">Hello 파일 시작 부분의 hello TrustFrameworkExtensions.xml이이 요소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

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

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="dd9d4-148">4 단계: TrustFrameworkExtensions.xml 사용자 프로필 편집 사용자 여정에서 오케스트레이션 단계로 hello REST 서비스 클레임 교환이 포함</span><span class="sxs-lookup"><span data-stu-id="dd9d4-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="dd9d4-149">단계 추가 toohello 프로필 편집 사용자 여행, hello 사용자 후에 (오케스트레이션 1-4 단계에서 다음과 같은 XML hello)를 인증 하 고 hello 사용자가 업데이트 하는 hello 프로필 정보 (5 단계)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="dd9d4-150">오케스트레이션 단계로 hello REST API 호출에 사용 될 수 있는 많은 사용 사례 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="dd9d4-151">오케스트레이션 단계로,이 클래스는 사용자 처음 등록 같은 작업을 성공적으로 완료 된 후 업데이트 tooan 외부 시스템으로 사용할 수 있습니다 또는 프로필로 동기화 tookeep 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="dd9d4-152">이 경우 hello 프로필 편집 후 toohello 응용 프로그램을 제공 하는 사용 되는 tooaugment hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="dd9d4-153">Hello 내 hello TrustFrameworkBase.xml 파일 tooyour TrustFrameworkExtensions.xml 파일에서 사용자의 여행 XML 코드를 편집 하는 hello 프로필 복사 `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="dd9d4-154">6 단계에서 수정 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="dd9d4-155">Hello 순서 버전와 일치 하지 않으면 경우 hello 하기 전에 hello 단계로 hello 코드를 삽입 하는 있는지 확인 `ClaimsExchange` 형식 `SendClaims`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="dd9d4-156">hello hello 사용자 작업에 대 한 최종 XML 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-156">hello final XML for hello user journey should look like this:</span></span>

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

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="dd9d4-157">5 단계: 추가 hello 클레임 `city` hello 클레임 tooyour 응용 프로그램 보내도록 tooyour 신뢰 당사자 정책 파일</span><span class="sxs-lookup"><span data-stu-id="dd9d4-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="dd9d4-158">ProfileEdit.xml 신뢰 당사자 (RP) 파일을 편집 하 고 hello를 수정할 `<TechnicalProfile Id="PolicyProfile">` 요소 tooadd hello 다음: `<OutputClaim ClaimTypeReferenceId="city" />`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="dd9d4-159">Hello 새 클레임을 추가한 후 hello 기술 프로필은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-159">After you add hello new claim, hello technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="dd9d4-160">6단계 - 변경 내용 업로드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="dd9d4-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="dd9d4-161">기존 버전의 hello 정책 hello를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="dd9d4-162">(선택 사항:) 계속 진행 하기 전에 hello 기존 버전 (다운로드) 하 여 확장 파일의 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="dd9d4-163">tookeep hello 초기 복잡성 낮은 hello 확장 파일의 여러 버전을 업로드 하지 않는 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="dd9d4-164">(선택 사항:) Hello hello 정책 파일 편집에 대 한 hello 정책 ID의 새 버전을 변경 하 여 이름 바꾸기 `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="dd9d4-165">Hello 확장 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="dd9d4-166">Hello 정책 편집 RP 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="dd9d4-167">사용 하 여 **지금 실행** tootest hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="dd9d4-168">IEF hello 검토 hello 토큰 toohello 응용 프로그램을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="dd9d4-169">모든 설정이 올바른지, hello 토큰 hello 새 클레임을 포함 됩니다 `city`, hello 값을 가진 `Redmond`합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dd9d4-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd9d4-170">Next steps</span></span>

[<span data-ttu-id="dd9d4-171">유효성 검증 단계로 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="dd9d4-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="dd9d4-172">Hello 프로필 편집 toogather 추가 정보를 사용자가 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd9d4-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
