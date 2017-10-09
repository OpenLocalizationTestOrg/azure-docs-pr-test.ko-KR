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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="26121-103">Azure Active Directory B2C: 사용자 지정 정책을 사용하여 ID 공급자로 MSA(Microsoft 계정) 추가</span><span class="sxs-lookup"><span data-stu-id="26121-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="26121-104">이 문서에서는 어떻게 tooenable 로그인 Microsoft 계정 (MSA)에서 사용자에 대 한 hello 사용을 통해 [사용자 지정 정책을](active-directory-b2c-overview-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26121-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="26121-105">Prerequisites</span></span>
<span data-ttu-id="26121-106">Hello에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="26121-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="26121-107">이러한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="26121-107">These steps include:</span></span>

1.  <span data-ttu-id="26121-108">Microsoft 계정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="26121-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="26121-109">Hello Microsoft 계정이 응용 프로그램 키 tooAzure AD B2C 추가</span><span class="sxs-lookup"><span data-stu-id="26121-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="26121-110">클레임 공급자 tooa 정책 추가</span><span class="sxs-lookup"><span data-stu-id="26121-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="26121-111">Hello Microsoft 계정 클레임 공급자의 tooa 사용자 여행을 등록 하는 중</span><span class="sxs-lookup"><span data-stu-id="26121-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="26121-112">테 넌 트 hello 정책 tooan Azure AD B2C 업로드 하 고 테스트</span><span class="sxs-lookup"><span data-stu-id="26121-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="26121-113">Microsoft 계정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="26121-113">Create a Microsoft account application</span></span>
<span data-ttu-id="26121-114">(Azure AD) Azure Active Directory B2C에 대 한 id 공급자로 toouse Microsoft 계정, Microsoft 계정 응용 프로그램 toocreate 필요 하 고 hello 오른쪽 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="26121-115">Microsoft 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-115">You need a Microsoft account.</span></span> <span data-ttu-id="26121-116">계정이 없는 경우 [https://www.live.com/](https://www.live.com/)을 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="26121-117">Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) Microsoft 계정 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="26121-118">**앱 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-118">Click **Add an app**.</span></span>

    ![Microsoft 계정 - 앱 추가](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="26121-120">응용 프로그램에 **이름**을 제공하고 **전자 메일로 연락하고**, **시작하도록 지원 받기**의 선택을 취소하고, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Microsoft 계정 - 응용 프로그램 등록](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="26121-122">hello 값을 복사 **응용 프로그램 Id**합니다. 필요한 tooconfigure Microsoft 계정을 id 공급자로 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26121-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Microsoft 계정-응용 프로그램 Id의 hello 값 복사](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="26121-124">**플랫폼 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-124">Click on **Add platform**</span></span>

    ![Microsoft 계정 - 플랫폼 추가](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="26121-126">Hello 플랫폼 목록에서 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-126">From hello platform list, choose **Web**.</span></span>

    ![Microsoft 계정-hello 플랫폼 목록에서 선택 웹](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="26121-128">입력 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **리디렉션 Uri** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="26121-129">**{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="26121-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Microsoft 계정 - 리디렉션 URL 설정](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="26121-131">클릭 **새 암호를 생성할** hello에서 **응용 프로그램 암호** 섹션.</span><span class="sxs-lookup"><span data-stu-id="26121-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="26121-132">Hello 화면에 표시 되는 새 암호를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="26121-133">필요한 tooconfigure Microsoft 계정을 id 공급자로 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26121-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="26121-134">이 암호는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-134">This password is an important security credential.</span></span>

    ![Microsoft 계정-새 암호 생성](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft 계정-복사 hello에 대 한 새 암호](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="26121-137">Hello 확인란의 **라이브 SDK 지원** hello에서 **고급 옵션** 섹션.</span><span class="sxs-lookup"><span data-stu-id="26121-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="26121-138">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-138">Click **Save**.</span></span>

    ![Microsoft 계정-Live SDK 지원](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="26121-140">Hello Microsoft 계정이 응용 프로그램 키 tooAzure AD B2C 추가</span><span class="sxs-lookup"><span data-stu-id="26121-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="26121-141">Microsoft 계정으로 페더레이션 hello 응용 프로그램 대신 Microsoft 계정 tootrust Azure AD B2C에 대 한 클라이언트 암호에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="26121-142">Azure AD B2C 테 넌 트에 Microsoft 계정이 응용 프로그램 secert toostore 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="26121-143">Tooyour Azure AD B2C 테 넌 트를 이동 하 고 선택 **B2C 설정** > **Id 경험 프레임 워크**</span><span class="sxs-lookup"><span data-stu-id="26121-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="26121-144">선택 **정책 키** 테 넌 트에 사용할 수 있는 tooview hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="26121-145">**+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="26121-146">**옵션**에는 **수동**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="26121-147">**이름**에는 `MSASecret`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="26121-148">hello 접두사 `B2C_1A_` 자동으로 추가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26121-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="26121-149">Hello에 **비밀** 상자 https://apps.dev.microsoft.com에서 Microsoft 응용 프로그램 암호를 입력 합니다</span><span class="sxs-lookup"><span data-stu-id="26121-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="26121-150">**키 사용**에는 **서명**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="26121-151">**만들기**</span><span class="sxs-lookup"><span data-stu-id="26121-151">Click **Create**</span></span>
9.  <span data-ttu-id="26121-152">Hello 키를 만든 확인 `B2C_1A_MSASecret`합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="26121-153">확장 정책에서 클레임 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="26121-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="26121-154">Microsoft 계정을 사용 하 여 사용자가 toosign의 하려는 경우를 클레임 공급자로 toodefine Microsoft 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="26121-155">즉, Azure AD B2C와 통신 하는 끝점 toospecify를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="26121-156">hello 끝점은 특정 사용자가 인증 하는 Azure AD B2C tooverify에서 사용 되는 클레임 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="26121-157">확장 정책 파일에서 `<ClaimsProvider>` 노드를 추가하여 Microsoft 계정을 클레임 공급자로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="26121-158">작업 디렉터리부터 hello 확장명 정책 파일 (TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="26121-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="26121-159">XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="26121-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="26121-160">Hello `<ClaimsProviders>` 섹션</span><span class="sxs-lookup"><span data-stu-id="26121-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="26121-161">Hello 아래 XML 조각 다음 추가 `ClaimsProviders` 요소:</span><span class="sxs-lookup"><span data-stu-id="26121-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

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

4.  <span data-ttu-id="26121-162">`client_id` 값을 Microsoft 계정 응용 프로그램 클라이언트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="26121-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="26121-163">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="26121-164">Hello 클레임 공급자 tooSign Microsoft 계정 또는 사용자 여행 로그인 등록</span><span class="sxs-lookup"><span data-stu-id="26121-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="26121-165">이 시점에서 hello id 공급자 설정 되어 있지만 hello 로그-up/로그인 화면 중에서 사용할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="26121-166">이제 tooadd hello Microsoft 계정 id 공급자 tooyour 사용자 필요한 `SignUpOrSignIn` 사용자 여행 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="26121-167">toomake 기존 템플릿 사용자 여행 중복 만듭니다 사용할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="26121-168">Hello Microsoft 계정 id 공급자로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="26121-169">Hello 이전에 복사한 경우 `<UserJourneys>` 정책 toohello 확장 프로그램 파일의 기본 파일에서 요소 `TrustFrameworkExtensions.xml`, toothis 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26121-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="26121-170">Hello 정책 (예를 들어 TrustFrameworkBase.xml)의 기본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="26121-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="26121-171">Hello `<UserJourneys>` 의 요소와 복사 hello 전체 내용을 `<UserJourneys>` 노드.</span><span class="sxs-lookup"><span data-stu-id="26121-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="26121-172">Hello 확장 파일 (예를 들어 TrustFrameworkExtensions.xml)를 열고 hello `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="26121-173">존재 하지 않으면 hello 요소 하나를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="26121-174">전체 내용을 hello `<UserJournesy>` hello의 자식으로 복사한 노드 `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="26121-175">디스플레이 hello 단추</span><span class="sxs-lookup"><span data-stu-id="26121-175">Display hello button</span></span>
<span data-ttu-id="26121-176">hello `<ClaimsProviderSelections>` 요소 hello 클레임 공급자 선택 옵션 목록 및 해당 순서를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="26121-177">`<ClaimsProviderSelection>`요소는 로그-up/로그인 페이지에 유사한 tooan identity provider 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="26121-178">추가 하는 경우는 `<ClaimsProviderSelection>` Microsoft 계정에 대 한 요소, 사용자 hello 페이지에 처음 삽입 새 단추 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="26121-179">tooadd이이 요소:</span><span class="sxs-lookup"><span data-stu-id="26121-179">tooadd this element:</span></span>

1.  <span data-ttu-id="26121-180">Hello `<UserJourney>` 포함 된 노드 `Id="SignUpOrSignIn"` 복사한 hello 사용자 여정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="26121-181">Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="26121-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="26121-182">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="26121-183">링크 hello 단추 tooan 동작</span><span class="sxs-lookup"><span data-stu-id="26121-183">Link hello button tooan action</span></span>
<span data-ttu-id="26121-184">Toolink 필요한 위치에 있는 단추를가지고 그 tooan 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="26121-185">hello 동작이 경우 Microsoft 계정 tooreceive와 Azure AD B2C toocommunicate에 대 한 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="26121-186">Microsoft 계정 클레임 공급자에 대 한 hello 기술 프로필을 연결 하 여 hello 단추 tooan 동작을 연결할:</span><span class="sxs-lookup"><span data-stu-id="26121-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="26121-187">Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.</span><span class="sxs-lookup"><span data-stu-id="26121-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="26121-188">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="26121-189">Hello 확인 `Id` 의과 같은 값인 hello에 `TargetClaimsExchangeId` hello 앞 섹션에서</span><span class="sxs-lookup"><span data-stu-id="26121-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="26121-190">확인 `TechnicalProfileReferenceId` 이전 (MSA OIDC)를 만든 toohello 기술 프로필 ID가 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26121-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="26121-191">Hello 정책 tooyour 테 넌 트에 업로드</span><span class="sxs-lookup"><span data-stu-id="26121-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="26121-192">Hello에 [Azure 포털](https://portal.azure.com), hello를 전환 [Azure AD B2C 테 넌 트의 상황에 맞는](active-directory-b2c-navigate-to-b2c-context.md), 및 열기 hello **Azure AD B2C** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="26121-193">**ID 경험 프레임워크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="26121-194">열기 hello **모든 정책** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="26121-195">**정책 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="26121-196">확인 **있으면 hello 정책 덮어쓰기** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="26121-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="26121-197">**업로드** TrustFrameworkExtensions.xml hello 유효성 검사가 발생 하지 않도록 하 고</span><span class="sxs-lookup"><span data-stu-id="26121-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="26121-198">지금 실행에 사용 하 여 hello 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="26121-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="26121-199">열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="26121-200">**지금 실행** hello 테 넌 트에 응용 프로그램이 하나 이상 toobe 미리 등록 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="26121-201">toolearn tooregister 응용 프로그램을 확인 하려면 어떻게 해야 Azure AD B2C hello [시작](active-directory-b2c-get-started.md) 문서 또는 hello [응용 프로그램 등록](active-directory-b2c-app-registration.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="26121-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="26121-202">열기 **B2C_1A_signup_signin**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="26121-203">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="26121-204">Microsoft 계정을 사용 하 여 수 toosign 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="26121-205">[선택 사항] Hello Microsoft 계정 클레임 공급자의 tooProfile 편집 사용자 여행 등록</span><span class="sxs-lookup"><span data-stu-id="26121-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="26121-206">좋습니다 tooadd hello Microsoft 계정 id 공급자도 tooyour 사용자 `ProfileEdit` 사용자 여행 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="26121-207">toomake 마지막 두 단계 hello 반복 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26121-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="26121-208">디스플레이 hello 단추</span><span class="sxs-lookup"><span data-stu-id="26121-208">Display hello button</span></span>
1.  <span data-ttu-id="26121-209">정책 (예를 들어 TrustFrameworkExtensions.xml) hello 확장 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="26121-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="26121-210">Hello `<UserJourney>` 포함 된 노드 `Id="ProfileEdit"` 복사한 hello 사용자 여정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="26121-211">Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="26121-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="26121-212">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="26121-213">링크 hello 단추 tooan 동작</span><span class="sxs-lookup"><span data-stu-id="26121-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="26121-214">Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.</span><span class="sxs-lookup"><span data-stu-id="26121-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="26121-215">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="26121-216">지금 실행에 사용 하 여 hello 사용자 지정 프로필 편집 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="26121-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="26121-217">열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="26121-218">열기 **B2C_1A_ProfileEdit**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="26121-219">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="26121-220">Microsoft 계정을 사용 하 여 수 toosign 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="26121-221">Hello 완성 된 정책 파일을 다운로드</span><span class="sxs-lookup"><span data-stu-id="26121-221">Download hello complete policy files</span></span>
<span data-ttu-id="26121-222">선택 사항: 권장 사용자 고유의 사용자 지정 정책 파일을 사용 하 여 이러한 샘플 파일을 사용 하는 대신 안내 사용자 지정 정책을 사용 하 여 시작 하는 hello를 완료 한 후 시나리오를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="26121-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="26121-223">참조할 샘플 정책 파일</span><span class="sxs-lookup"><span data-stu-id="26121-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
