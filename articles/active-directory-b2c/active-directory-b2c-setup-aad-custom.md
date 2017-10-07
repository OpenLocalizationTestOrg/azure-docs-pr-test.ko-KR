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
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="f3657-103">Azure Active Directory B2C: Azure AD 계정을 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="f3657-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="f3657-104">이 문서에서는 어떻게 tooenable 로그인 hello 사용을 통해 특정 Azure Active Directory (Azure AD) 조직의 사용자에 대 한 [사용자 지정 정책을](active-directory-b2c-overview-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3657-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f3657-105">Prerequisites</span></span>

<span data-ttu-id="f3657-106">Hello에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="f3657-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="f3657-107">이러한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-107">These steps include:</span></span>

1. <span data-ttu-id="f3657-108">Azure AD B2C(Azure Active Directory B2C) 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="f3657-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="f3657-109">Azure AD B2C 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f3657-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="f3657-110">두 개의 정책 엔진 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="f3657-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="f3657-111">키 설정</span><span class="sxs-lookup"><span data-stu-id="f3657-111">Setting up keys.</span></span>
5. <span data-ttu-id="f3657-112">Hello 스타터 팩을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="f3657-113">Azure AD 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f3657-113">Create an Azure AD app</span></span>

<span data-ttu-id="f3657-114">tooenable 로그인 특정 사용자에 대 한 Azure AD 조직 tooregister hello 조직 Azure AD 테 넌 트 내에서 응용 프로그램을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="f3657-115">Hello 조직 Azure AD 테 넌 트 및 "fabrikamb2c.onmicrosoft.com"에 대 한 "contoso.com" 지침을 진행 하는 hello에 hello Azure AD B2C 테 넌 트로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="f3657-116">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="f3657-117">Hello 위쪽 막대에서 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-117">On hello top bar, select your account.</span></span> <span data-ttu-id="f3657-118">Hello에서 **디렉터리** 목록 tooregister 원하는 hello 조직 Azure AD 테 넌 트 응용 프로그램 (contoso.com)을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="f3657-119">선택 **더 많은 서비스** hello 왼쪽된 창에서 "응용 프로그램 등록 합니다."에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="f3657-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="f3657-120">**새 응용 프로그램 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="f3657-121">응용 프로그램의 이름(예: `Azure AD B2C App`)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="f3657-122">선택 **웹 응용 프로그램 / API** hello 응용 프로그램 종류에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="f3657-123">에 대 한 **로그온 URL**, hello url을 입력 합니다. 여기서 `yourtenant` Azure AD B2C 테 넌 트의 hello 이름으로 바뀝니다 (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="f3657-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="f3657-124">Save hello 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-124">Save hello application ID.</span></span>
1. <span data-ttu-id="f3657-125">새로 만든 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="f3657-126">Hello에서 **설정** 블레이드를 **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="f3657-127">새 키를 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-127">Create a new key, and save it.</span></span> <span data-ttu-id="f3657-128">Hello 다음 섹션의 hello 단계에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="f3657-129">Azure AD hello 키 tooAzure AD B2C 추가</span><span class="sxs-lookup"><span data-stu-id="f3657-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="f3657-130">Azure AD B2C 테 넌 트의 toostore hello contoso.com 응용 프로그램 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="f3657-131">toodo이:</span><span class="sxs-lookup"><span data-stu-id="f3657-131">toodo this:</span></span>
1. <span data-ttu-id="f3657-132">Tooyour Azure AD B2C 테 넌 트를 이동 하 고 선택 **B2C 설정** > **Id 경험 프레임 워크** > **정책 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="f3657-133">**+추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-133">Select **+Add**.</span></span>
1. <span data-ttu-id="f3657-134">다음 옵션을 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-134">Select or enter these options:</span></span>
   * <span data-ttu-id="f3657-135">**수동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-135">Select **Manual**.</span></span>
   * <span data-ttu-id="f3657-136">**이름**에 대해 Azure AD 테넌트 이름과 일치하는 이름(예: `ContosoAppSecret`)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="f3657-137">hello 접두사 `B2C_1A_` 키의 toohello 이름을 자동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="f3657-138">Hello에 응용 프로그램에 키 붙여넣기 **비밀** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="f3657-139">**서명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-139">Select **Signature**.</span></span>
1. <span data-ttu-id="f3657-140">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-140">Select **Create**.</span></span>
1. <span data-ttu-id="f3657-141">Hello 키를 만든 확인 `B2C_1A_ContosoAppSecret`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="f3657-142">기본 정책에서 클레임 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="f3657-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="f3657-143">Azure AD를 사용 하 여 사용자가 toosign의 하려는 경우 Azure AD를 클레임 공급자로 toodefine를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="f3657-144">즉, Azure AD B2C와 통신 하는 끝점 toospecify를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="f3657-145">hello 끝점에서 특정 사용자가 인증 하는 Azure AD B2C tooverify 사용 되는 클레임 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="f3657-146">Azure AD toohello를 추가 하 여 Azure AD를 클레임 공급자로 정의할 수 있습니다 `<ClaimsProvider>` 정책 hello 확장 파일에 있는 노드:</span><span class="sxs-lookup"><span data-stu-id="f3657-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="f3657-147">작업 디렉터리부터 hello 확장 파일 (TrustFrameworkExtensions.xml)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="f3657-148">Hello `<ClaimsProviders>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="f3657-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="f3657-149">존재 하지 않는 경우 hello 루트 노드에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="f3657-150">다음과 같이 새로운 `<ClaimsProvider>` 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="f3657-151">Hello에서 `<ClaimsProvider>` 노드를 업데이트 hello 값에 대 한 `<Domain>` tooa 고유 값 toodistinguish 사용된 될 수 있는 기타 id 공급자에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="f3657-152">Hello에서 `<ClaimsProvider>` 노드를 업데이트 hello 값에 대 한 `<DisplayName>` tooa 이름을 hello에 대 한 클레임 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="f3657-153">이 값은 현재 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="f3657-154">Hello 기술 프로필 업데이트</span><span class="sxs-lookup"><span data-stu-id="f3657-154">Update hello technical profile</span></span>

<span data-ttu-id="f3657-155">tooget hello Azure AD 끝점에서 토큰을 Azure AD와 Azure AD B2C toocommunicate를 사용 해야 함을 toodefine hello 프로토콜 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="f3657-156">Hello 내부 이렇게 `<TechnicalProfile>` 요소의 `<ClaimsProvider>`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="f3657-157">업데이트의 hello hello ID `<TechnicalProfile>` 노드.</span><span class="sxs-lookup"><span data-stu-id="f3657-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="f3657-158">이 ID가 사용 되는 toorefer toothis hello 정책의 다른 부분과에서 기술 프로필.</span><span class="sxs-lookup"><span data-stu-id="f3657-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="f3657-159">에 대 한 hello 시간 `<DisplayName>`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="f3657-160">이 값은 hello 로그인 단추 로그인 화면에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="f3657-161">에 대 한 hello 시간 `<Description>`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="f3657-162">Hello OpenID Connect 프로토콜을 사용 하 여 azure AD를 구분 하므로 해당 hello 값에 대 한 `<Protocol>` 은 `"OpenIdConnect"`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="f3657-163">Tooupdate hello 필요한 `<Metadata>` hello XML 파일 섹션에에서 특정에 대 한 tooearlier tooreflect hello 구성 설정 참조 Azure AD 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="f3657-164">Hello XML 파일에서 hello 메타 데이터 값을 다음과 같이 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="f3657-165">설정 `<Item Key="METADATA">` 너무`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`여기서 `yourAzureADtenant` 은 Azure AD 테 넌 트 이름 (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="f3657-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="f3657-166">브라우저와 go toohello 열고 `METADATA` 방금 업데이트 하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="f3657-167">Hello 브라우저에서 hello 'issuer' 개체에 대 한 확인 하 고 해당 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="f3657-168">Hello 다음과 같이 표시 됩니다: `https://sts.windows.net/{tenantId}/`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="f3657-169">에 대 한 hello 값을 붙여 `<Item Key="ProviderName">` hello XML 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="f3657-170">설정 `<Item Key="client_id">` hello 응용 프로그램 등록 시와에서 toohello 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="f3657-171">설정 `<Item Key="IdTokenAudience">` hello 응용 프로그램 등록 시와에서 toohello 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="f3657-172">되도록 `<Item Key="response_types">` 너무 설정`id_token`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="f3657-173">되도록 `<Item Key="UsePolicyInRedirectUri">` 너무 설정`false`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="f3657-174">또한 Azure AD B2C 테 넌 트 toohello Azure AD에에서 등록 toolink hello Azure AD 암호 해야 `<ClaimsProvider>` 정보:</span><span class="sxs-lookup"><span data-stu-id="f3657-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="f3657-175">Hello에 `<CryptographicKeys>` hello 앞에 XML 파일 섹션에 대 한 hello 시간, `StorageReferenceId` toohello 참조 ID가 정의 된 hello 암호 (예를 들어 `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="f3657-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="f3657-176">확인에 대 한 hello 확장 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="f3657-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="f3657-177">지금까지 구성한 정책을 Azure AD B2C 알 수 있도록 방법을 Azure AD 디렉터리와 toocommunicate 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="f3657-178">없다는 문제 지금까지 사용자 정책 정당한 tooconfirm의 hello 확장 파일을 업로드 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f3657-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="f3657-179">toodo 하므로:</span><span class="sxs-lookup"><span data-stu-id="f3657-179">toodo so:</span></span>

1. <span data-ttu-id="f3657-180">열기 hello **모든 정책** 블레이드 Azure AD B2C 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="f3657-181">Hello 확인 **있으면 hello 정책 덮어쓰기** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="f3657-182">Hello 확장 파일 (TrustFrameworkExtensions.xml)를 업로드 하 고 hello 유효성 검사 실패 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="f3657-183">Hello Azure AD 클레임 공급자의 tooa 사용자 여행 등록</span><span class="sxs-lookup"><span data-stu-id="f3657-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="f3657-184">사용자 친구의 tooadd hello Azure AD identity provider tooone를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="f3657-185">이 시점에서 hello id 공급자 설정 되어 있지만 hello 로그-up/로그인 화면 중에서 사용할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="f3657-186">toomake 사용할 수 있는 것 기존 템플릿 사용자 여행 중복 만들어져 hello Azure AD id 공급자를 포함 되도록 한 다음 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="f3657-187">Hello 정책 (예를 들어 TrustFrameworkBase.xml)의 기본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="f3657-188">Hello `<UserJourneys>` 전체 요소와 복사 hello `<UserJourney>` 포함 된 노드 `Id="SignUpOrSignIn"`합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="f3657-189">Hello 확장 파일 (예를 들어 TrustFrameworkExtensions.xml)를 열고 hello `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="f3657-190">존재 하지 않으면 hello 요소 하나를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="f3657-191">전체 붙여넣기 hello `<UserJourney>` hello의 자식으로 복사한 노드 `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="f3657-192">새 사용자의 hello 여행의 hello ID 이름 바꾸기 (으로 이름 바꾸기 예를 들어 `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="f3657-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="f3657-193">디스플레이 hello "button"</span><span class="sxs-lookup"><span data-stu-id="f3657-193">Display hello "button"</span></span>

<span data-ttu-id="f3657-194">hello `<ClaimsProviderSelection>` 요소 로그-up/로그인 화면에 유사한 tooan identity provider 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="f3657-195">추가 하는 경우는 `<ClaimsProviderSelection>` Azure AD에 대 한 요소, 사용자 hello 페이지에 처음 삽입 새 단추 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="f3657-196">tooadd이이 요소:</span><span class="sxs-lookup"><span data-stu-id="f3657-196">tooadd this element:</span></span>

1. <span data-ttu-id="f3657-197">Hello `<OrchestrationStep>` 포함 된 노드 `Order="1"` 방금 만든 hello 사용자 여정에서.</span><span class="sxs-lookup"><span data-stu-id="f3657-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="f3657-198">Hello 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="f3657-199">설정 `TargetClaimsExchangeId` tooan 적절 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="f3657-200">다음과 같은 hello 권장 다른 사용자와 규칙:  *\[ClaimProviderName\]Exchange*합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="f3657-201">링크 hello 단추 tooan 동작</span><span class="sxs-lookup"><span data-stu-id="f3657-201">Link hello button tooan action</span></span>

<span data-ttu-id="f3657-202">Toolink 필요한 위치에 있는 단추를가지고 그 tooan 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="f3657-203">hello 동작이 경우 Azure AD tooreceive와 Azure AD B2C toocommunicate에 대 한 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="f3657-204">Azure AD 클레임 공급자에 대 한 hello 기술 프로필을 연결 하 여 hello 단추 tooan 동작을 연결할:</span><span class="sxs-lookup"><span data-stu-id="f3657-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="f3657-205">Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.</span><span class="sxs-lookup"><span data-stu-id="f3657-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="f3657-206">Hello 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="f3657-207">업데이트 `Id` 의과 같은 값인 toohello `TargetClaimsExchangeId` hello 섹션 앞에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="f3657-208">업데이트 `TechnicalProfileReferenceId` toohello ID의 기술 hello 프로필 앞에서 만든 (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="f3657-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="f3657-209">Hello 업데이트 된 확장 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="f3657-209">Upload hello updated extension file</span></span>

<span data-ttu-id="f3657-210">Hello 확장 파일을 수정 하 고 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="f3657-211">저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-211">Save it.</span></span> <span data-ttu-id="f3657-212">그런 다음 hello 파일을 업로드 하 고 성공 하는 모든 유효성 검사를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="f3657-213">Hello RP 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="f3657-213">Update hello RP file</span></span>

<span data-ttu-id="f3657-214">이제 tooupdate hello 신뢰 당사자 (RP)에 파일이 필요 방금 만든 hello 사용자 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="f3657-215">작업 디렉터리에 SignUpOrSignIn.xml의 복사본을 만들고 이름을 바꿉니다 (예를 들어 이름을 tooSignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="f3657-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="f3657-216">열기 hello 새 파일 및 업데이트 hello `PolicyId` 특성 `<TrustFrameworkPolicy>` 고유 값 (예를 들어 SignUpOrSignInWithAAD)으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="f3657-217">이 정책 hello 이름 됩니다 (예를 들어 B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="f3657-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="f3657-218">Hello 수정 `ReferenceId` 특성 `<DefaultUserJourney>` toomatch hello ID (SignUpOrSignUsingContoso) 하 여 만든 hello 새 사용자 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="f3657-219">변경 내용을 저장 하 고 hello 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f3657-220">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f3657-220">Troubleshooting</span></span>

<span data-ttu-id="f3657-221">해당 블레이드를 열고 클릭 하 여 방금 업로드 hello 사용자 지정 정책을 테스트 **지금 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="f3657-222">toodiagnose 문제에 대해 알아보세요 [문제 해결](active-directory-b2c-troubleshoot-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3657-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f3657-223">Next steps</span></span>

<span data-ttu-id="f3657-224">피드백을 너무 제공[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f3657-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
