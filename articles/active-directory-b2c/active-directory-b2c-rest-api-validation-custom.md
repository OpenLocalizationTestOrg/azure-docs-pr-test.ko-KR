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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="fe3ca-103">연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 사용자 입력에 대한 유효성 검사로 통합</span><span class="sxs-lookup"><span data-stu-id="fe3ca-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="fe3ca-104">Identity 경험 프레임 워크 (IEF) Azure Active Directory B2C 기반이 되는 hello (Azure AD B2C) hello identity 개발자 toointegrate 사용자 여정에서 RESTful API와의 상호 작용을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="fe3ca-105">이 연습의 hello 끝 수 toocreate RESTful 서비스와 상호 작용 하는 Azure AD B2C 사용자 때 고려해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="fe3ca-106">hello IEF 데이터를 보내고 클레임의 클레임에 있는 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="fe3ca-107">hello API와 상호 작용을 hello:</span><span class="sxs-lookup"><span data-stu-id="fe3ca-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="fe3ca-108">API와 상호 작용을 오케스트레이션 단계 내부에서 발생하는 REST API 클레임 교환 또는 유효성 검사 프로필로 설계할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="fe3ca-109">일반적으로 hello 사용자의 입력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-109">Typically validates input from hello user.</span></span> <span data-ttu-id="fe3ca-110">Hello 사용자 로부터 hello 값이 거부 되 면 tooenter hello 기회 tooreturn 오류 메시지를 사용 하 여 유효한 값 hello 사용자 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="fe3ca-111">또한 오케스트레이션 단계로 hello 상호 작용을 디자인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="fe3ca-112">자세한 내용은 [연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 오케스트레이션 단계로 통합](active-directory-b2c-rest-api-step-custom.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="fe3ca-113">예: hello 유효성 검사 프로필 hello 프로필 편집 사용자 여행 ProfileEdit.xml hello 스타터 팩 파일에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="fe3ca-114">Hello hello 프로필에는 사용자가 편집에 속하지 않는 한 제외 목록을 제공 해당 hello 이름을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe3ca-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fe3ca-115">Prerequisites</span></span>

- <span data-ttu-id="fe3ca-116">Azure AD B2C 테 넌 트 구성 toocomplete 로그-up/로그인에 설명 된 대로 로컬 계정 [시작](active-directory-b2c-get-started-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="fe3ca-117">사용 REST API 끝점 toointeract 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="fe3ca-118">이 연습에서는 REST API 서비스를 사용하여 [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/)라는 데모 사이트를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="fe3ca-119">1 단계: 준비 hello REST API 함수</span><span class="sxs-lookup"><span data-stu-id="fe3ca-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="fe3ca-120">REST API 함수는 설치 방법은이 문서의 hello 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="fe3ca-121">[Azure 기능](https://docs.microsoft.com/azure/azure-functions/functions-reference) 뛰어난 toolkit hello 클라우드에서 toocreate RESTful 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="fe3ca-122">`playerTag`로 예상하는 클레임을 받는 Azure 함수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="fe3ca-123">hello 함수는이 클레임의 존재 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="fe3ca-124">Hello 완전 한 Azure 함수 코드에 액세스할 수 있습니다 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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

<span data-ttu-id="fe3ca-125">hello IEF hello에서는 `userMessage` 클레임 해당 hello Azure 함수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="fe3ca-126">이 클레임 409 충돌 상태 앞 예제는 hello에 반환 될 때와 같은 hello 유효성 검사가 실패 하면 문자열 toohello 사용자로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="fe3ca-127">2 단계: TrustFrameworkExtensions.xml 파일에서 기술 프로필로 hello RESTful API 클레임 exchange 구성</span><span class="sxs-lookup"><span data-stu-id="fe3ca-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="fe3ca-128">기술 프로필은 RESTful 서비스 hello로 원하는 hello 교환의 hello 전체 구성.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="fe3ca-129">Hello TrustFrameworkExtensions.xml 파일을 열고 다음 XML 조각 hello 내 hello 추가 `<ClaimsProviders>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="fe3ca-130">다음과 같은 XML을 RESTful 공급자 hello에 `Version=1.0.0.0` hello 프로토콜 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="fe3ca-131">이 hello 외부 서비스와 상호 작용 하는 hello 함수도 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="fe3ca-132">hello `InputClaims` 요소 hello IEF toohello REST 서비스에서에서 전송 될 hello 클레임을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="fe3ca-133">이 예제에서는 hello 클레임의 내용을 hello `givenName` toohello REST 서비스를 받게 될 `playerTag`합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="fe3ca-134">이 예제에서는 hello IEF에 필요 하지 않으면 다시 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="fe3ca-135">대신, 응답을 수신 하는 hello 상태 코드에 따라 작업을 실행 하 고 hello REST 서비스에 대 한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="fe3ca-136">3 단계: toovalidate hello 사용자 입력을 원하는 자체 어설션된 기술 프로필에 hello RESTful 서비스 클레임 교환이 포함</span><span class="sxs-lookup"><span data-stu-id="fe3ca-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="fe3ca-137">사용자와 상호 작용 hello hello hello 유효성 검사 단계의 가장 일반적인 용도가입니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="fe3ca-138">여기서 hello 사용자는 입력 예상된 tooprovide 모든 상호 작용은 *기술 프로필 자체 어설션된*합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="fe3ca-139">예를 들어 hello 유효성 검사 toohello 자체 Asserted ProfileUpdate 기술 프로필을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="fe3ca-140">이 신뢰 당사자 (RP) 정책 파일 hello hello 기술 프로필 `Profile Edit` 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="fe3ca-141">tooadd hello 클레임 exchange toohello 자체 기술 프로필 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="fe3ca-142">파일을 열고 hello TrustFrameworkBase.xml을 검색할 `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="fe3ca-143">이 기술 프로필의 hello 구성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="fe3ca-144">클레임 (입력된 클레임) hello 사용자의 요청 수 및 hello 자체 어설션된 공급자 (출력 클레임 포함)에서 다시 예상할 수 있는 클레임으로 hello 사용자와 hello exchange가 정의 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="fe3ca-145">`TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`를 검색하고 이 프로필이 `<UserJourney Id="ProfileEdit">`의 6 오케스트레이션 단계로 호출되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="fe3ca-146">4 단계: 업로드 하 고 hello 프로필 편집 RP 정책 파일을 테스트</span><span class="sxs-lookup"><span data-stu-id="fe3ca-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="fe3ca-147">Hello 새 버전의 hello TrustFrameworkExtensions.xml 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="fe3ca-148">사용 하 여 **지금 실행** tootest hello 프로필 RP 정책 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="fe3ca-149">Hello에 hello 기존 이름 (예를 들어 mcvinny) 중 하나를 제공 하 여 hello 유효성 검사 테스트 **지정 된 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="fe3ca-150">모든 설정이 올바른지, 알리는 hello 사용자 hello 플레이어 태그가 이미 사용 될 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe3ca-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe3ca-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe3ca-151">Next steps</span></span>

[<span data-ttu-id="fe3ca-152">Hello 프로필 편집 및 사용자 등록 toogather 추가 정보에서 사용자 수정</span><span class="sxs-lookup"><span data-stu-id="fe3ca-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="fe3ca-153">연습: Azure AD B2C 사용자 경험에서 REST API 클레임 교환을 오케스트레이션 단계로 통합</span><span class="sxs-lookup"><span data-stu-id="fe3ca-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
