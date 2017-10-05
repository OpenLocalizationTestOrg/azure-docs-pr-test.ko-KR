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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="22216-103">연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 오케스트레이션 단계로 통합</span><span class="sxs-lookup"><span data-stu-id="22216-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="22216-104">Azure AD B2C(Azure Active Directory B2C)의 기반이 되는 IEF(ID 경험 프레임워크)를 사용하면 ID 개발자가 사용자 경험에서 RESTful API와의 상호 작용을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="22216-105">이 연습의 끝부분에서는 RESTful 서비스와 상호 작용하는 Azure AD B2C 사용자 경험을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="22216-106">IEF는 클레임으로 데이터를 보내고 다시 클레임으로 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="22216-107">REST API 클레임 교환에서는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="22216-108">오케스트레이션 단계로 설계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="22216-109">외부 동작을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-109">Can trigger an external action.</span></span> <span data-ttu-id="22216-110">예를 들어 외부 데이터베이스에 이벤트를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="22216-111">값을 가져와서 사용자 데이터베이스에 저장하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="22216-112">받은 클레임은 나중에 실행 흐름을 변경하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="22216-113">또한 상호 작용은 유효성 검사 프로필로 설계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="22216-114">자세한 내용은 [연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 사용자 입력에 대한 유효성 검사로 통합](active-directory-b2c-rest-api-validation-custom.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22216-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="22216-115">시나리오는 사용자가 프로필 편집을 수행할 때 다음을 수행하려고 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22216-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="22216-116">외부 시스템에서 사용자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="22216-117">해당 사용자를 등록한 도시를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="22216-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="22216-118">해당 특성을 클레임으로 응용 프로그램에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22216-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="22216-119">Prerequisites</span></span>

- <span data-ttu-id="22216-120">[시작](active-directory-b2c-get-started-custom.md)에서 설명한 대로 로컬 계정 등록/로그인을 완료하도록 구성된 Azure AD B2C 테넌트</span><span class="sxs-lookup"><span data-stu-id="22216-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="22216-121">상호 작용할 REST API 끝점</span><span class="sxs-lookup"><span data-stu-id="22216-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="22216-122">이 연습에서는 간단한 웹후크 Azure 함수 앱을 예제로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="22216-123">*권장*: [유효성 검증 단계로 REST API 클레임 교환을](active-directory-b2c-rest-api-validation-custom.md) 완료</span><span class="sxs-lookup"><span data-stu-id="22216-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="22216-124">1단계 - REST API 함수 준비</span><span class="sxs-lookup"><span data-stu-id="22216-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="22216-125">REST API 함수 설정은 이 문서의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="22216-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="22216-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference)는 클라우드에서 RESTful 서비스를 만들 수 있는 뛰어난 도구 키트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="22216-127">`email`이라는 클레임을 받고 할당된 `Redmond` 값이 포함된 `city` 클레임을 반환하는 Azure 함수를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="22216-128">샘플 Azure 함수는 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="22216-129">Azure 함수에서 반환하는 `userMessage` 클레임은 이 컨텍스트에서 선택 사항이며 IEF에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22216-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="22216-130">이 클레임은 잠재적으로 응용 프로그램에 전달되고 나중에 사용자에게 표시되는 메시지로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="22216-131">Azure 함수 앱을 사용하면 특정 함수의 식별자를 포함하여 함수 URL을 쉽게 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="22216-132">이 경우 URL은 https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==이며,</span><span class="sxs-lookup"><span data-stu-id="22216-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="22216-133">테스트 용도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="22216-134">2단계 - TrustFrameworkExtensions.xml 파일에서 RESTful API 클레임 교환을 기술 프로필로 구성</span><span class="sxs-lookup"><span data-stu-id="22216-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="22216-135">기술적 프로필은 RESTful 서비스에서 원하는 교환의 전체 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="22216-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="22216-136">TrustFrameworkExtensions.xml 파일을 열고 `<ClaimsProvider>` 요소 내에 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="22216-137">다음 XML에서 `Version=1.0.0.0` RESTful 공급자는 프로토콜로 설명되며,</span><span class="sxs-lookup"><span data-stu-id="22216-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="22216-138">외부 서비스와 상호 작용할 함수로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="22216-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="22216-139">`<InputClaims>` 요소는 IEF에서 REST 서비스로 전송할 클레임을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="22216-140">이 예제에서는 REST 서비스에 `givenName` 클레임의 내용을 `email` 클레임으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="22216-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="22216-141">`<OutputClaims>` 요소는 IEF가 REST 서비스에서 예상하는 클레임을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="22216-142">받은 클레임 수에 관계 없이 IEF에서는 여기서 식별된 클레임만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="22216-143">이 예제에서는 `city`로 받은 클레임이 `city`라는 IEF 클레임에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="22216-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="22216-144">3단계 - TrustFrameworkExtensions.xml 파일의 스키마에 새 `city` 클레임 추가</span><span class="sxs-lookup"><span data-stu-id="22216-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="22216-145">`city` 클레임은 아직 스키마의 어디에서도 정의되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="22216-146">따라서 `<BuildingBlocks>` 요소 내에 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="22216-147">이 요소는 TrustFrameworkExtensions.xml 파일의 시작 부분에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="22216-148">4단계 - TrustFrameworkExtensions.xml에서 REST 서비스 클레임 교환을 프로필 편집 사용자 경험의 오케스트레이션 단계로 포함</span><span class="sxs-lookup"><span data-stu-id="22216-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="22216-149">사용자가 인증되고(다음 XML의 1-4 오케스트레이션 단계) 업데이트된 프로필 정보를 제공하면(5단계) 프로필 편집 사용자 경험에 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="22216-150">REST API 호출을 오케스트레이션 단계로 사용할 수 있는 사용 사례가 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="22216-151">오케스트레이션 단계로서 사용자가 첫 번째 등록과 같은 태스크를 성공적으로 완료한 후 외부 시스템에 대한 업데이트로 사용하거나 동기화된 정보 상태로 유지하기 위한 프로필 업데이트로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="22216-152">이 경우 프로필 편집 후에 응용 프로그램에 제공된 정보를 보강하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="22216-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="22216-153">TrustFrameworkBase.xml 파일의 프로필 편집 사용자 경험 XML 코드를 `<UserJourneys>` 요소의 TrustFrameworkExtensions.xml 파일로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="22216-154">그런 다음 6단계에서 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="22216-155">순서가 사용자의 버전과 일치하지 않으면 코드를 `ClaimsExchange` 형식 `SendClaims` 앞의 단계로 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="22216-156">사용자 경험의 최종 XML은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="22216-157">5단계 - `city` 클레임을 신뢰 당사자 정책 파일에 추가하여 응용 프로그램에 해당 클레임을 보냄</span><span class="sxs-lookup"><span data-stu-id="22216-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="22216-158">ProfileEdit.xml RP(신뢰 당사자) 파일을 편집하고 `<TechnicalProfile Id="PolicyProfile">` 요소를 수정하여 `<OutputClaim ClaimTypeReferenceId="city" />`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="22216-159">새 클레임을 추가한 후에 기술 프로필은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="22216-160">6단계 - 변경 내용 업로드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="22216-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="22216-161">기존 버전의 정책을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="22216-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="22216-162">(선택 사항) 계속하기 전에 기존 버전의 확장 파일을 다운로드하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="22216-163">초기 복잡성을 낮추려면 여러 버전의 확장 파일을 업로드하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="22216-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="22216-164">(선택 사항) `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`를 변경하여 정책 편집 파일에 대한 새 버전의 정책 ID의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22216-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="22216-165">확장 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="22216-166">정책 편집 RP 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="22216-167">**지금 실행**을 사용하여 정책을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="22216-168">IEF에서 응용 프로그램에 반환하는 토큰을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="22216-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="22216-169">모든 항목이 올바르게 설정되면 토큰에는 `Redmond` 값의 새 클레임 `city`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="22216-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="22216-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22216-170">Next steps</span></span>

[<span data-ttu-id="22216-171">유효성 검증 단계로 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="22216-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="22216-172">프로필 편집을 수정하여 사용자로부터 추가 정보 수집</span><span class="sxs-lookup"><span data-stu-id="22216-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
