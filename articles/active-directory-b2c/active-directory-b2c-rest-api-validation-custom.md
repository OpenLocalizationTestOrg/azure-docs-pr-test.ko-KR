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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="062a2-103">연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 사용자 입력에 대한 유효성 검사로 통합</span><span class="sxs-lookup"><span data-stu-id="062a2-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="062a2-104">Azure AD B2C(Azure Active Directory B2C)의 기반이 되는 IEF(ID 경험 프레임워크)를 사용하면 ID 개발자가 사용자 경험에서 RESTful API와의 상호 작용을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="062a2-105">이 연습의 끝부분에서는 RESTful 서비스와 상호 작용하는 Azure AD B2C 사용자 경험을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="062a2-106">IEF는 클레임으로 데이터를 보내고 다시 클레임으로 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="062a2-107">API와의 상호 작용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-107">The interaction with the API:</span></span>

- <span data-ttu-id="062a2-108">API와 상호 작용을 오케스트레이션 단계 내부에서 발생하는 REST API 클레임 교환 또는 유효성 검사 프로필로 설계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="062a2-109">일반적으로 사용자 입력의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-109">Typically validates input from the user.</span></span> <span data-ttu-id="062a2-110">사용자의 값이 거부되면 사용자는 오류 메시지를 반환하는 기회와 함께 유효한 값을 다시 입력하려고 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="062a2-111">또한 상호 작용은 오케스트레이션 단계로도 설계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="062a2-112">자세한 내용은 [연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 오케스트레이션 단계로 통합](active-directory-b2c-rest-api-step-custom.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="062a2-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="062a2-113">유효성 검사 프로필 예제의 경우 ProfileEdit.xml 시작 팩 파일에서 프로필 편집 사용자 경험을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="062a2-114">프로필 편집에서 사용자가 제공한 이름이 제외 목록에 속하지 않은 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="062a2-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="062a2-115">Prerequisites</span></span>

- <span data-ttu-id="062a2-116">[시작](active-directory-b2c-get-started-custom.md)에서 설명한 대로 로컬 계정 등록/로그인을 완료하도록 구성된 Azure AD B2C 테넌트</span><span class="sxs-lookup"><span data-stu-id="062a2-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="062a2-117">상호 작용할 REST API 끝점</span><span class="sxs-lookup"><span data-stu-id="062a2-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="062a2-118">이 연습에서는 REST API 서비스를 사용하여 [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/)라는 데모 사이트를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="062a2-119">1단계 - REST API 함수 준비</span><span class="sxs-lookup"><span data-stu-id="062a2-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="062a2-120">REST API 함수 설정은 이 문서의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="062a2-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference)는 클라우드에서 RESTful 서비스를 만들 수 있는 뛰어난 도구 키트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="062a2-122">`playerTag`로 예상하는 클레임을 받는 Azure 함수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="062a2-123">함수는 이 클레임의 존재 여부에 대한 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="062a2-124">전체 Azure Function 코드는 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="062a2-125">IEF는 Azure 함수에서 반환하는 `userMessage` 클레임을 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="062a2-126">위의 예제에서는 409 충돌 상태가 반환된 경우와 같이 유효성 검사에 실패하면 이 클레임이 사용자에게 문자열로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="062a2-127">2단계 - TrustFrameworkExtensions.xml 파일에서 RESTful API 클레임 교환을 기술 프로필로 구성</span><span class="sxs-lookup"><span data-stu-id="062a2-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="062a2-128">기술적 프로필은 RESTful 서비스에서 원하는 교환의 전체 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="062a2-129">TrustFrameworkExtensions.xml 파일을 열고 `<ClaimsProviders>` 요소 내에 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="062a2-130">다음 XML에서 `Version=1.0.0.0` RESTful 공급자는 프로토콜로 설명되며,</span><span class="sxs-lookup"><span data-stu-id="062a2-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="062a2-131">외부 서비스와 상호 작용할 함수로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="062a2-132">`InputClaims` 요소는 IEF에서 REST 서비스로 전송할 클레임을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="062a2-133">이 예제에서는 REST 서비스에 `givenName` 클레임의 내용을 `playerTag`로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="062a2-134">그리고 IEF에서 클레임을 다시 예상하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="062a2-135">대신 REST 서비스의 응답을 기다리고, 받는 상태 코드에 따라 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="062a2-136">3단계 - 사용자 입력의 유효성을 검사하려는 자체 어설션된 기술 프로필에 RESTful 서비스 클레임 교환을 포함</span><span class="sxs-lookup"><span data-stu-id="062a2-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="062a2-137">유효성 검사의 가장 일반적인 용도는 사용자와의 상호 작용입니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="062a2-138">사용자가 입력을 제공해야 하는 모든 상호 작용은 *자체 어설션된 기술 프로필*입니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="062a2-139">이 예제에서는 Self-Asserted-ProfileUpdate 기술 프로필에 유효성 검사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="062a2-140">이는 `Profile Edit` RP(신뢰 당사자) 정책 파일에서 사용하는 기술 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="062a2-141">자체 어설션된 기술 프로필에 클레임 교환을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="062a2-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="062a2-142">TrustFrameworkBase 파일을 열고 `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="062a2-143">이 기술 프로필의 구성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="062a2-144">사용자와의 교환이 사용자에게 요청할 클레임(입력 클레임) 및 자체 어설션된 공급자에서 반환될 클레임(출력 클레임)으로 정의되는 방식을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="062a2-145">`TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`를 검색하고 이 프로필이 `<UserJourney Id="ProfileEdit">`의 6 오케스트레이션 단계로 호출되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="062a2-146">4단계 - 프로필 편집 RP 정책 파일 업로드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="062a2-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="062a2-147">새 버전의 TrustFrameworkExtensions.xml 정책 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="062a2-148">**지금 실행**을 사용하여 프로필 편집 RP 정책 파일을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="062a2-149">**지정된 이름** 필드에 기존 이름(예: mcvinny) 중 하나를 제공하여 유효성 검사를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="062a2-150">모든 항목이 올바르게 설정되면 플레이어 태그가 이미 사용되었음을 사용자에게 알리는 메시지를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="062a2-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="062a2-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="062a2-151">Next steps</span></span>

[<span data-ttu-id="062a2-152">프로필 편집 및 사용자 등록을 수정하여 사용자로부터 추가 정보 수집</span><span class="sxs-lookup"><span data-stu-id="062a2-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="062a2-153">연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 오케스트레이션 단계로 통합</span><span class="sxs-lookup"><span data-stu-id="062a2-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
