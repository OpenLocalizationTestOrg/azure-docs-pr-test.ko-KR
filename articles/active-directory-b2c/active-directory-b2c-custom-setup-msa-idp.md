---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 ID 공급자로 MSA(Microsoft 계정) 추가"
description: "OIDC(Microsoft OpenID 연결) 프로토콜을 사용하는 ID 공급자로 Microsoft를 사용하는 샘플"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 8c981046ff41d3927ff60d6dc4f40366ae25ba74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="13017-103">Azure Active Directory B2C: 사용자 지정 정책을 사용하여 ID 공급자로 MSA(Microsoft 계정) 추가</span><span class="sxs-lookup"><span data-stu-id="13017-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="13017-104">이 문서에서는 [사용자 지정 정책](active-directory-b2c-overview-custom.md)을 사용하여 MSA(Microsoft 계정)의 사용자가 로그인할 수 있도록 하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-104">This article shows you how to enable sign-in for users from Microsoft account (MSA) through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13017-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="13017-105">Prerequisites</span></span>
<span data-ttu-id="13017-106">[사용자 지정 정책 시작](active-directory-b2c-get-started-custom.md) 문서의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="13017-107">이러한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-107">These steps include:</span></span>

1.  <span data-ttu-id="13017-108">Microsoft 계정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="13017-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="13017-109">Azure AD B2C에 Microsoft 계정 응용 프로그램 키 추가</span><span class="sxs-lookup"><span data-stu-id="13017-109">Adding the Microsoft account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="13017-110">정책에 클레임 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="13017-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="13017-111">사용자 경험에 Microsoft 계정 클레임 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="13017-111">Registering the Microsoft Account claims provider to a user journey</span></span>
5.  <span data-ttu-id="13017-112">Azure AD B2C 테넌트에 정책 업로드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="13017-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="13017-113">Microsoft 계정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="13017-113">Create a Microsoft account application</span></span>
<span data-ttu-id="13017-114">Azure AD(Active Directory) B2C에서 Microsoft 계정을 ID 공급자로 사용하려면 먼저 Microsoft 계정 응용 프로그램을 만들고 올바른 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-114">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="13017-115">Microsoft 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-115">You need a Microsoft account.</span></span> <span data-ttu-id="13017-116">계정이 없는 경우 [https://www.live.com/](https://www.live.com/)을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="13017-117">[Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)로 이동하고 Microsoft 계정 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-117">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="13017-118">**앱 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-118">Click **Add an app**.</span></span>

    ![Microsoft 계정 - 앱 추가](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="13017-120">응용 프로그램에 **이름**을 제공하고 **전자 메일로 연락하고**, **시작하도록 지원 받기**의 선택을 취소하고, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Microsoft 계정 - 응용 프로그램 등록](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="13017-122">**응용 프로그램 ID**의 값을 복사합니다. 테넌트에서 Microsoft 계정을 ID 공급자로 구성하려면 그 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-122">Copy the value of **Application Id**. You need it to configure Microsoft account as an identity provider in your tenant.</span></span>

    ![Microsoft 계정 - 응용 프로그램 ID의 값 복사](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="13017-124">**플랫폼 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-124">Click on **Add platform**</span></span>

    ![Microsoft 계정 - 플랫폼 추가](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="13017-126">플랫폼 목록에서 **웹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-126">From the platform list, choose **Web**.</span></span>

    ![Microsoft 계정 - 플랫폼 목록에서 웹 선택](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="13017-128">**URI 리디렉션** 필드에 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="13017-129">**{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="13017-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Microsoft 계정 - 리디렉션 URL 설정](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="13017-131">**응용 프로그램 비밀** 섹션 아래에서 **새 암호 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-131">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="13017-132">화면에 표시되는 새 암호를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-132">Copy the new password displayed on screen.</span></span> <span data-ttu-id="13017-133">테넌트에서 Microsoft 계정을 ID 공급자로 구성하려면 그 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-133">You need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="13017-134">이 암호는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="13017-134">This password is an important security credential.</span></span>

    ![Microsoft 계정-새 암호 생성](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft 계정 - 새 암호 복사](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="13017-137">**고급 옵션** 섹션 아래에서 **Live SDK 지원**라는 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-137">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="13017-138">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-138">Click **Save**.</span></span>

    ![Microsoft 계정-Live SDK 지원](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-the-microsoft-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="13017-140">Azure AD B2C에 Microsoft 계정 응용 프로그램 키 추가</span><span class="sxs-lookup"><span data-stu-id="13017-140">Add the Microsoft account application key to Azure AD B2C</span></span>
<span data-ttu-id="13017-141">Microsoft 계정으로 페더레이션하려면 응용 프로그램 대신 Azure AD B2C를 신뢰하기 위해 Microsoft 계정에 대한 클라이언트 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-141">Federation with Microsoft accounts requires a client secret for Microsoft account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="13017-142">Azure AD B2C 테넌트에 Microsoft 계정 응용 프로그램 비밀을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-142">You need to store your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="13017-143">Azure AD B2C 테넌트로 이동하고 **B2C 설정** > **ID 경험 프레임워크**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-143">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="13017-144">**정책 키**를 선택하여 테넌트에 사용 가능한 키를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="13017-144">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="13017-145">**+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="13017-146">**옵션**에는 **수동**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="13017-147">**이름**에는 `MSASecret`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="13017-148">`B2C_1A_` 접두사가 자동으로 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-148">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="13017-149">**비밀** 상자에서 https://apps.dev.microsoft.com의 Microsoft 응용 프로그램 암호를 입력합니다</span><span class="sxs-lookup"><span data-stu-id="13017-149">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="13017-150">**키 사용**에는 **서명**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="13017-151">**만들기**</span><span class="sxs-lookup"><span data-stu-id="13017-151">Click **Create**</span></span>
9.  <span data-ttu-id="13017-152">`B2C_1A_MSASecret` 키를 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-152">Confirm that you've created the key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="13017-153">확장 정책에서 클레임 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="13017-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="13017-154">사용자가 Microsoft 계정을 사용하여 로그인하도록 하려면 Microsoft 계정을 클레임 공급자로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-154">If you want users to sign in by using Microsoft Account, you need to define Microsoft Account as a claims provider.</span></span> <span data-ttu-id="13017-155">즉, Azure AD B2C가 통신하는 끝점을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-155">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="13017-156">끝점은 Azure AD B2C에서 사용하는 일련의 클레임을 제공하여 특정 사용자가 인증했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-156">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="13017-157">확장 정책 파일에서 `<ClaimsProvider>` 노드를 추가하여 Microsoft 계정을 클레임 공급자로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="13017-158">작업 디렉터리에서 확장 정책 파일(TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13017-158">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="13017-159">XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="13017-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="13017-160">`<ClaimsProviders>` 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-160">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="13017-161">`ClaimsProviders` 요소 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-161">Add following XML snippet under the `ClaimsProviders` element:</span></span>

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  <span data-ttu-id="13017-162">`client_id` 값을 Microsoft 계정 응용 프로그램 클라이언트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="13017-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="13017-163">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-163">Save the file.</span></span>

## <a name="register-the-microsoft-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="13017-164">등록 또는 로그인 사용자 경험에 Microsoft 계정 클레임 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="13017-164">Register the Microsoft Account claims provider to Sign up or Sign-in user journey</span></span>

<span data-ttu-id="13017-165">이 시점에서 ID 공급자가 설정되었지만 등록/로그인 화면에서 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-165">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="13017-166">이제 `SignUpOrSignIn` 사용자 경험에 Microsoft 계정 ID 공급자를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-166">Now you need to add the Microsoft Account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="13017-167">사용할 수 있도록 하려면 기존 템플릿 사용자 경험의 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13017-167">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="13017-168">Microsoft 계정 ID 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-168">Then we add the Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="13017-169">앞에서 `<UserJourneys>` 요소를 정책의 기본 파일에서 `TrustFrameworkExtensions.xml` 확장 파일로 복사한 경우 이 섹션으로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-169">If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file `TrustFrameworkExtensions.xml`, you can skip to this section.</span></span>

1.  <span data-ttu-id="13017-170">정책의 기본 파일(예: TrustFrameworkBase.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13017-170">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="13017-171">`<UserJourneys>` 요소를 찾고 `<UserJourneys>` 노드의 전체 콘텐츠를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-171">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="13017-172">확장 파일(예: TrustFrameworkExtensions.xml)을 열고 `<UserJourneys>` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-172">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="13017-173">요소가 존재하지 않는 경우 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-173">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="13017-174">복사한 `<UserJournesy>` 노드의 전체 콘텐츠를 `<UserJourneys>` 요소의 자식으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-174">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="13017-175">단추 표시</span><span class="sxs-lookup"><span data-stu-id="13017-175">Display the button</span></span>
<span data-ttu-id="13017-176">`<ClaimsProviderSelections>` 요소는 클레임 공급자 선택 옵션 목록과 해당 순서를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-176">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="13017-177">`<ClaimsProviderSelection>` 요소는 등록/로그인 페이지에서 ID 공급자 단추를 사용하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-177">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="13017-178">Microsoft 계정에 `<ClaimsProviderSelection>` 요소를 추가하면 사용자가 페이지를 열 때 새 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13017-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="13017-179">이 요소를 추가하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-179">To add this element:</span></span>

1.  <span data-ttu-id="13017-180">복사한 사용자 경험에서 `Id="SignUpOrSignIn"`이 포함된 `<UserJourney>` 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-180">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="13017-181">`Order="1"`이 포함된 `<OrchestrationStep>` 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-181">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="13017-182">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="13017-183">작업에 단추 연결</span><span class="sxs-lookup"><span data-stu-id="13017-183">Link the button to an action</span></span>
<span data-ttu-id="13017-184">이제 단추가 준비되었으므로 동작에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-184">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="13017-185">이 경우에 작업을 통해 Azure AD B2C에서 Microsoft 계정과 통신하여 토큰을 수신할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13017-185">The action, in this case, is for Azure AD B2C to communicate with Microsoft Account to receive a token.</span></span> <span data-ttu-id="13017-186">Microsoft 계정 클레임 공급자의 기술 프로필을 연결하여 동작에 단추를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-186">Link the button to an action by linking the technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="13017-187">`<UserJourney>` 노드에 `Order="2"`가 포함된 `<OrchestrationStep>`을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-187">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="13017-188">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="13017-189">`Id`에 이전 섹션의 `TargetClaimsExchangeId`와 동일한 값이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-189">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
>   * <span data-ttu-id="13017-190">`TechnicalProfileReferenceId` ID를 이전에 만든 기술 프로필로(MSA-OIDC)로 설정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-190">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="13017-191">테넌트에 정책 업로드</span><span class="sxs-lookup"><span data-stu-id="13017-191">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="13017-192">[Azure Portal](https://portal.azure.com)에서 [Azure AD B2C 테넌트의 컨텍스트](active-directory-b2c-navigate-to-b2c-context.md)로 전환하고 **Azure AD B2C** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13017-192">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="13017-193">**ID 경험 프레임워크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="13017-194">**모든 정책** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13017-194">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="13017-195">**정책 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="13017-196">**정책이 있는 경우 덮어쓰기** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-196">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="13017-197">TrustFrameworkExtensions.xml을 **업로드**하고 유효성 검사가 실패하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="13017-198">지금 실행을 사용하여 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="13017-198">Test the custom policy by using Run Now</span></span>

1.  <span data-ttu-id="13017-199">**Azure AD B2C 설정**을 열고 **ID 경험 프레임워크**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-199">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="13017-200">**지금 실행**을 사용하려면 하나 이상의 응용 프로그램이 테넌트에 미리 등록되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-200">**Run now** requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="13017-201">응용 프로그램을 등록하는 방법은 Azure AD B2C [시작](active-directory-b2c-get-started.md) 문서 또는 [응용 프로그램 등록](active-directory-b2c-app-registration.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13017-201">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="13017-202">업로드한 RP(신뢰 당사자) 사용자 지정 정책인 **B2C_1A_signup_signin**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13017-202">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="13017-203">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="13017-204">Microsoft 계정을 사용하여 로그인할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-204">You should be able to sign in using Microsoft account.</span></span>

## <a name="optional-register-the-microsoft-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="13017-205">[선택 사항]프로필 편집 사용자 경험에 Microsoft 계정 클레임 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="13017-205">[Optional] Register the Microsoft Account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="13017-206">`ProfileEdit` 사용자 경험에 Microsoft 계정 ID 공급자를 추가하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-206">You may want to add the Microsoft Account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="13017-207">사용할 수 있도록 하려면 마지막 두 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-207">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="13017-208">단추 표시</span><span class="sxs-lookup"><span data-stu-id="13017-208">Display the button</span></span>
1.  <span data-ttu-id="13017-209">정책의 확장 파일(예: TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13017-209">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="13017-210">복사한 사용자 경험에서 `Id="ProfileEdit"`이 포함된 `<UserJourney>` 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-210">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="13017-211">`Order="1"`이 포함된 `<OrchestrationStep>` 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-211">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="13017-212">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="13017-213">작업에 단추 연결</span><span class="sxs-lookup"><span data-stu-id="13017-213">Link the button to an action</span></span>
1.  <span data-ttu-id="13017-214">`<UserJourney>` 노드에 `Order="2"`가 포함된 `<OrchestrationStep>`을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-214">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="13017-215">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="13017-216">지금 실행을 사용하여 사용자 지정 프로필-편집 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="13017-216">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="13017-217">**Azure AD B2C 설정**을 열고 **ID 경험 프레임워크**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-217">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="13017-218">업로드한 RP(신뢰 당사자) 사용자 지정 정책인 **B2C_1A_ProfileEdit**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="13017-218">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="13017-219">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="13017-220">Microsoft 계정을 사용하여 로그인할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13017-220">You should be able to sign in using Microsoft account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="13017-221">완성 정책 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="13017-221">Download the complete policy files</span></span>
<span data-ttu-id="13017-222">선택 사항: 이러한 샘플 파일을 사용하는 대신 사용자 지정 정책을 사용하여 시작을 완료한 후에 고유한 사용자 지정 정책 사용하여 시나리오를 빌드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="13017-222">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="13017-223">참조할 샘플 정책 파일</span><span class="sxs-lookup"><span data-stu-id="13017-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
