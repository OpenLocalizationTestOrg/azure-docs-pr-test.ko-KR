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
ms.openlocfilehash: 6c073d70debfdc3560405955d65fa9ccaa7d8b1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="2b0bb-103">Azure Active Directory B2C: Azure AD 계정을 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="2b0bb-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="2b0bb-104">이 문서에서는 [사용자 지정 정책](active-directory-b2c-overview-custom.md)을 사용하여 특정 Azure AD(Azure Active Directory) 조직의 사용자에 대한 로그인을 사용하도록 설정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b0bb-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2b0bb-105">Prerequisites</span></span>

<span data-ttu-id="2b0bb-106">[사용자 지정 정책 시작](active-directory-b2c-get-started-custom.md) 문서의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="2b0bb-107">이러한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-107">These steps include:</span></span>

1. <span data-ttu-id="2b0bb-108">Azure AD B2C(Azure Active Directory B2C) 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="2b0bb-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="2b0bb-109">Azure AD B2C 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2b0bb-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="2b0bb-110">두 개의 정책 엔진 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="2b0bb-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="2b0bb-111">키 설정</span><span class="sxs-lookup"><span data-stu-id="2b0bb-111">Setting up keys.</span></span>
5. <span data-ttu-id="2b0bb-112">시작 팩 설정</span><span class="sxs-lookup"><span data-stu-id="2b0bb-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="2b0bb-113">Azure AD 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2b0bb-113">Create an Azure AD app</span></span>

<span data-ttu-id="2b0bb-114">특정 Azure AD 조직의 사용자에 대한 로그인을 사용하도록 설정하려면 조직의 Azure AD 테넌트 내에 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="2b0bb-115">조직의 Azure AD 테넌트로 "contoso.com"을 사용하고, 다음 지침에서는 "fabrikamb2c.onmicrosoft.com"을 Azure AD B2C 테넌트로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="2b0bb-116">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2b0bb-117">위쪽 막대에서 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-117">On the top bar, select your account.</span></span> <span data-ttu-id="2b0bb-118">**디렉터리** 목록에서 응용 프로그램을 등록하려는 조직의 Azure AD 테넌트(contoso.com)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
1. <span data-ttu-id="2b0bb-119">왼쪽 창에서 **더 많은 서비스**를 클릭하고 "앱 등록"을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="2b0bb-120">**새 응용 프로그램 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="2b0bb-121">응용 프로그램의 이름(예: `Azure AD B2C App`)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="2b0bb-122">응용 프로그램 종류에 대해 **웹앱/API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-122">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="2b0bb-123">**로그온 URL**에 대해 다음 URL을 입력합니다. 여기서 `yourtenant`는 Azure AD B2C 테넌트의 이름(`fabrikamb2c.onmicrosoft.com`)으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="2b0bb-124">응용 프로그램 ID를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-124">Save the application ID.</span></span>
1. <span data-ttu-id="2b0bb-125">새로 만든 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-125">Select the newly created application.</span></span>
1. <span data-ttu-id="2b0bb-126">**설정** 블레이드 아래에서 **키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-126">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="2b0bb-127">새 키를 만들고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-127">Create a new key, and save it.</span></span> <span data-ttu-id="2b0bb-128">이 키는 다음 섹션의 단계에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-128">You will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="2b0bb-129">Azure AD B2C에 Azure AD 키 추가</span><span class="sxs-lookup"><span data-stu-id="2b0bb-129">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="2b0bb-130">Azure AD B2C 테넌트에 contoso.com 응용 프로그램 키를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-130">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="2b0bb-131">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-131">To do this:</span></span>
1. <span data-ttu-id="2b0bb-132">Azure AD B2C 테넌트로 이동하고 **B2C 설정** > **ID 경험 프레임워크** > **정책 키**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-132">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="2b0bb-133">**+추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-133">Select **+Add**.</span></span>
1. <span data-ttu-id="2b0bb-134">다음 옵션을 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-134">Select or enter these options:</span></span>
   * <span data-ttu-id="2b0bb-135">**수동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-135">Select **Manual**.</span></span>
   * <span data-ttu-id="2b0bb-136">**이름**에 대해 Azure AD 테넌트 이름과 일치하는 이름(예: `ContosoAppSecret`)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="2b0bb-137">`B2C_1A_` 접두사가 키의 이름에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-137">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="2b0bb-138">**비밀** 상자에서 응용 프로그램 키를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-138">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="2b0bb-139">**서명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-139">Select **Signature**.</span></span>
1. <span data-ttu-id="2b0bb-140">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-140">Select **Create**.</span></span>
1. <span data-ttu-id="2b0bb-141">`B2C_1A_ContosoAppSecret` 키를 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-141">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="2b0bb-142">기본 정책에서 클레임 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="2b0bb-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="2b0bb-143">사용자가 Azure AD를 사용하여 로그인하도록 하려면 Azure AD를 클레임 공급자로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-143">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="2b0bb-144">즉, Azure AD B2C가 통신하는 끝점을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-144">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="2b0bb-145">끝점은 Azure AD B2C에서 사용하는 일단의 클레임을 제공하여 특정 사용자가 인증했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-145">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="2b0bb-146">정책의 확장 파일에서 `<ClaimsProvider>` 노드에 Azure AD를 추가하여 Azure AD를 클레임 공급자로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-146">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="2b0bb-147">작업 디렉터리에서 확장 파일(TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-147">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="2b0bb-148">`<ClaimsProviders>` 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-148">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="2b0bb-149">존재하지 않는 경우 루트 노드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-149">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="2b0bb-150">다음과 같이 새로운 `<ClaimsProvider>` 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="2b0bb-151">`<ClaimsProvider>` 노드 아래에서 `<Domain>` 값을 다른 ID 공급자와 구분하는 데 사용할 수 있는 고유한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-151">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="2b0bb-152">`<ClaimsProvider>` 노드 아래에서 `<DisplayName>` 값을 클레임 공급자에게 친숙한 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-152">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="2b0bb-153">이 값은 현재 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-153">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="2b0bb-154">기술 프로필 업데이트</span><span class="sxs-lookup"><span data-stu-id="2b0bb-154">Update the technical profile</span></span>

<span data-ttu-id="2b0bb-155">Azure AD 끝점에서 토큰을 가져오려면 Azure AD B2C에서 Azure AD와 통신하는 데 사용해야 하는 프로토콜을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-155">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="2b0bb-156">이 작업은 `<ClaimsProvider>`의 `<TechnicalProfile>` 요소 내에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-156">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="2b0bb-157">`<TechnicalProfile>` 노드의 ID를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-157">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="2b0bb-158">이 ID는 정책의 다른 부분에서 이 기술 프로필을 참조하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-158">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="2b0bb-159">`<DisplayName>` 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-159">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="2b0bb-160">이 값은 로그인 화면의 로그인 단추에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-160">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="2b0bb-161">`<Description>` 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-161">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="2b0bb-162">Azure AD는 OpenID Connect 프로토콜을 사용하므로 `<Protocol>` 값이 `"OpenIdConnect"`인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-162">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="2b0bb-163">앞에서 언급한 XML의 `<Metadata>` 섹션을 업데이트하여 특정 Azure AD 테넌트의 구성 설정을 반영해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-163">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="2b0bb-164">XML 파일에서 다음과 같이 메타데이터 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-164">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="2b0bb-165">`<Item Key="METADATA">`를 `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`으로 설정합니다. 여기서 `yourAzureADtenant`는 Azure AD 테넌트 이름(예: contoso.com)입니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-165">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="2b0bb-166">브라우저를 열고 방금 업데이트한 `METADATA` URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-166">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="2b0bb-167">브라우저에서 '발급자' 개체를 찾아 해당 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-167">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="2b0bb-168">`https://sts.windows.net/{tenantId}/`과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-168">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="2b0bb-169">XML 파일에서 `<Item Key="ProviderName">` 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-169">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="2b0bb-170">앱 등록에서 `<Item Key="client_id">`를 응용 프로그램 ID로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-170">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="2b0bb-171">앱 등록에서 `<Item Key="IdTokenAudience">`를 응용 프로그램 ID로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-171">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="2b0bb-172">`<Item Key="response_types">`을 `id_token`로 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-172">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="2b0bb-173">`<Item Key="UsePolicyInRedirectUri">`을 `false`로 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="2b0bb-174">또한 Azure AD B2C 테넌트에 등록한 Azure AD 비밀을 Azure AD `<ClaimsProvider>` 정보에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-174">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="2b0bb-175">앞에서 언급한 XML 파일의 `<CryptographicKeys>` 섹션에서 `StorageReferenceId` 값을 정의한 비밀의 참조 ID(예: `ContosoAppSecret`)로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-175">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="2b0bb-176">확인을 위한 확장 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="2b0bb-176">Upload the extension file for verification</span></span>

<span data-ttu-id="2b0bb-177">지금까지 Azure AD B2C에서 Azure AD 디렉터리와 통신하는 방법을 알 수 있도록 정책을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-177">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="2b0bb-178">정책의 확장 파일을 업로드하여 지금까지 문제가 발생하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-178">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="2b0bb-179">이렇게 하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-179">To do so:</span></span>

1. <span data-ttu-id="2b0bb-180">Azure AD B2C 테넌트에서 **모든 정책** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-180">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="2b0bb-181">**정책이 있는 경우 덮어쓰기** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-181">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="2b0bb-182">확장 파일(TrustFrameworkExtensions.xml)을 업로드하고 유효성 검사가 실패하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-182">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="2b0bb-183">사용자 경험에 Azure AD 클레임 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="2b0bb-183">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="2b0bb-184">이제 사용자 경험 중 하나에 Azure AD ID 공급자를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-184">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="2b0bb-185">이 시점에서 ID 공급자가 설정되었지만 등록/로그인 화면에서 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-185">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="2b0bb-186">사용할 수 있게 하려면 기존 템플릿 사용자 경험의 복제본을 만든 다음 Azure AD ID 공급자도 포함하도록 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-186">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="2b0bb-187">정책의 기본 파일(예: TrustFrameworkBase.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-187">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="2b0bb-188">`<UserJourneys>` 요소를 찾고 `Id="SignUpOrSignIn"`을 포함한 `<UserJourney>` 노드 전체를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-188">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="2b0bb-189">확장 파일(예: TrustFrameworkExtensions.xml)을 열고 `<UserJourneys>` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-189">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="2b0bb-190">요소가 존재하지 않는 경우 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-190">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="2b0bb-191">복사한 `<UserJourney>` 노드 전체를 `<UserJourneys>` 요소의 자식으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-191">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="2b0bb-192">새 사용자 경험의 ID 이름을 바꿉니다(예: `SignUpOrSignUsingContoso`로 이름 바꾸기).</span><span class="sxs-lookup"><span data-stu-id="2b0bb-192">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="2b0bb-193">"단추" 표시</span><span class="sxs-lookup"><span data-stu-id="2b0bb-193">Display the "button"</span></span>

<span data-ttu-id="2b0bb-194">`<ClaimsProviderSelection>` 요소는 등록/로그인 화면에서 ID 공급자 단추를 사용하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-194">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="2b0bb-195">Azure AD에 `<ClaimsProviderSelection>` 요소를 추가하면 사용자가 페이지를 열 때 새 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="2b0bb-196">이 요소를 추가하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-196">To add this element:</span></span>

1. <span data-ttu-id="2b0bb-197">방금 만든 사용자 경험에서 `Order="1"`이 포함된 `<OrchestrationStep>` 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-197">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="2b0bb-198">다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-198">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="2b0bb-199">`TargetClaimsExchangeId`을 적절한 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-199">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="2b0bb-200">다른 값과 동일한 규칙인 *\[ClaimProviderName\]Exchange*를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-200">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="2b0bb-201">작업에 단추 연결</span><span class="sxs-lookup"><span data-stu-id="2b0bb-201">Link the button to an action</span></span>

<span data-ttu-id="2b0bb-202">이제 단추가 준비되었으므로 동작에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-202">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="2b0bb-203">이 경우에 작업을 통해 Azure AD B2C에서 Azure AD와 통신하여 토큰을 수신할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-203">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="2b0bb-204">Azure AD 클레임 공급자의 기술 프로필을 연결하여 동작에 단추를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-204">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="2b0bb-205">`<UserJourney>` 노드에 `Order="2"`가 포함된 `<OrchestrationStep>`을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-205">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="2b0bb-206">다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-206">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="2b0bb-207">`Id`를 이전 섹션의 `TargetClaimsExchangeId`와 동일한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-207">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="2b0bb-208">`TechnicalProfileReferenceId`를 이전에 만든 기술 프로필의 ID(예: ContosoProfile)로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-208">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="2b0bb-209">업데이트된 확장 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="2b0bb-209">Upload the updated extension file</span></span>

<span data-ttu-id="2b0bb-210">확장 파일을 수정하는 작업을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-210">You are done modifying the extension file.</span></span> <span data-ttu-id="2b0bb-211">저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-211">Save it.</span></span> <span data-ttu-id="2b0bb-212">그런 다음 파일을 업로드하고 모든 유효성 검사가 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-212">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="2b0bb-213">RP 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="2b0bb-213">Update the RP file</span></span>

<span data-ttu-id="2b0bb-214">이제 방금 만든 사용자 경험을 시작할 RP(신뢰 당사자) 파일을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-214">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="2b0bb-215">작업 디렉터리에 SignUpOrSignIn.xml의 복사본을 만들고 이름을 바꿉니다(예: SignUpOrSignInWithAAD.xml로 이름 바꾸기).</span><span class="sxs-lookup"><span data-stu-id="2b0bb-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="2b0bb-216">새 파일을 열고 `<TrustFrameworkPolicy>`의 `PolicyId` 특성을 고유한 값(예: SignUpOrSignInWithAAD)으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-216">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="2b0bb-217">이는 정책의 이름(예: B2C\_1A\_SignUpOrSignInWithAAD)입니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-217">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="2b0bb-218">만든 새 사용자 경험의 ID(SignUpOrSignUsingContoso)와 일치하도록 `<DefaultUserJourney>`의 `ReferenceId` 특성을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-218">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="2b0bb-219">변경 내용을 저장하고 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-219">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2b0bb-220">문제 해결</span><span class="sxs-lookup"><span data-stu-id="2b0bb-220">Troubleshooting</span></span>

<span data-ttu-id="2b0bb-221">해당 블레이드를 열고 **지금 실행**을 클릭하여 방금 업로드한 사용자 지정 정책을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-221">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="2b0bb-222">문제를 진단하려면 [문제 해결](active-directory-b2c-troubleshoot-custom.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-222">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b0bb-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b0bb-223">Next steps</span></span>

<span data-ttu-id="2b0bb-224">[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)에 대한 피드백을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b0bb-224">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
