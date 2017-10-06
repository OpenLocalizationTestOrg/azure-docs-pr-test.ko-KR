---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 OAuth2 ID 공급자로 Google+ 추가"
description: "OAuth2 프로토콜을 사용하여 ID 공급자로 Google+를 사용하는 샘플"
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
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="a159e-103">Azure Active Directory B2C: 사용자 지정 정책을 사용하여 OAuth2 ID 공급자로 Google+ 추가</span><span class="sxs-lookup"><span data-stu-id="a159e-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="a159e-104">이 가이드에서는 어떻게 tooenable 로그인 hello 사용을 통해 Google + 계정에서 사용자에 대 한 알아봅니다 [사용자 지정 정책을](active-directory-b2c-overview-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a159e-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a159e-105">Prerequisites</span></span>

<span data-ttu-id="a159e-106">Hello에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a159e-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="a159e-107">이러한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-107">These steps include:</span></span>

1.  <span data-ttu-id="a159e-108">Google+ 계정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a159e-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="a159e-109">Hello Google + 계정을 응용 프로그램 키 tooAzure AD B2C 추가</span><span class="sxs-lookup"><span data-stu-id="a159e-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="a159e-110">클레임 공급자 tooa 정책 추가</span><span class="sxs-lookup"><span data-stu-id="a159e-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="a159e-111">Hello Google + 계정 클레임 공급자 tooa 사용자 여행을 등록 하는 중</span><span class="sxs-lookup"><span data-stu-id="a159e-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="a159e-112">테 넌 트 hello 정책 tooan Azure AD B2C 업로드 하 고 테스트</span><span class="sxs-lookup"><span data-stu-id="a159e-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="a159e-113">Google+ 계정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a159e-113">Create a Google+ account application</span></span>
<span data-ttu-id="a159e-114">toouse Google + (Azure AD) Azure Active Directory B2C에을 id 공급자로 toocreate Google + 응용 프로그램에 필요 하 고이 hello 오른쪽 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="a159e-115">Google+ 응용 프로그램을 [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="a159e-116">Toohello 이동 [Google 개발자 콘솔](https://console.developers.google.com/) 및 Google + 계정 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="a159e-117">**프로젝트 만들기**를 클릭하고 **프로젝트 이름**을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="a159e-118">Hello 클릭 **프로젝트 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-118">Click on hello **Projects menu**.</span></span>

    ![Google+ 계정 - 프로젝트 선택](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="a159e-120">Hello 클릭 ** + ** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-120">Click on hello **+** button.</span></span>

    ![Google+ 계정 - 새 프로젝트 만들기](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="a159e-122">**프로젝트 이름**을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Google+ 계정 - 새 프로젝트](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="a159e-124">Hello 프로젝트 준비 될 때까지 기다렸다가 hello 클릭 **프로젝트 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Google + 계정-새 프로젝트 toouse 준비 될 때까지 대기](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="a159e-126">프로젝트 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-126">Click on your project name.</span></span>

    ![Google + 계정-선택 hello 새 프로젝트](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="a159e-128">클릭 **API 관리자** 클릭 하 고 **자격 증명** 왼쪽 탐색 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="a159e-129">Hello 클릭 **OAuth 동의 화면** hello 위쪽 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Google+ 계정 - OAuth 동의 화면 설정](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="a159e-131">유효한 **메일 주소**를 선택하거나 지정하고 **제품 이름**을 제공한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+ - 응용 프로그램 자격 증명](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="a159e-133">**새 자격 증명**을 클릭한 다음 **OAuth 클라이언트 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+ - 새 응용 프로그램 자격 증명 만들기](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="a159e-135">**응용 프로그램 형식**에서 **웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+ - 응용 프로그램 형식 선택](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="a159e-137">제공는 **이름** 응용 프로그램에 대 한 입력 `https://login.microsoftonline.com` hello에 **승인 된 자바 스크립트 원본** 필드 및 `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello에 **권한이 부여 된 리디렉션 URIs**필드입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="a159e-138">**{tenant}** 를 사용자의 테넌트 이름(예: contosob2c.onmicrosoft.com)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="a159e-139">hello **{tenant}** 값은 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="a159e-140">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-140">Click **Create**.</span></span>

    ![Google+ - 승인된 JavaScript 원본 및 리디렉션 URI 제공](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="a159e-142">Hello 값의 복사 **클라이언트 Id** 및 **클라이언트 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="a159e-143">테 넌 트를 id 공급자로 두 tooconfigure Google + 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="a159e-144">**클라이언트 암호** 는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-144">**Client secret** is an important security credential.</span></span>

    ![Google +-클라이언트 Id와 클라이언트 암호의 hello 값 복사](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="a159e-146">Hello Google + 계정을 응용 프로그램 키 tooAzure AD B2C 추가</span><span class="sxs-lookup"><span data-stu-id="a159e-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="a159e-147">Google + 계정으로 페더레이션 hello 응용 프로그램을 대신 하 여 Google + 계정 tootrust Azure AD B2C에 대 한 클라이언트 암호에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="a159e-148">Azure AD B2C 테 넌 트의 사용자 Google + 응용 프로그램 암호 toostore 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="a159e-149">Tooyour Azure AD B2C 테 넌 트를 이동 하 고 선택 **B2C 설정** > **Id 경험 프레임 워크**</span><span class="sxs-lookup"><span data-stu-id="a159e-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="a159e-150">선택 **정책 키** 테 넌 트에 사용할 수 있는 tooview hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="a159e-151">**+추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="a159e-152">**옵션**에는 **수동**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="a159e-153">**이름**에는 `GoogleSecret`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="a159e-154">hello 접두사 `B2C_1A_` 자동으로 추가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="a159e-155">Hello에 **비밀** 상자 https://apps.dev.microsoft.com에서 Microsoft 응용 프로그램 암호를 입력 합니다</span><span class="sxs-lookup"><span data-stu-id="a159e-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="a159e-156">**키 사용**에는 **서명**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="a159e-157">**만들기**</span><span class="sxs-lookup"><span data-stu-id="a159e-157">Click **Create**</span></span>
9.  <span data-ttu-id="a159e-158">Hello 키를 만든 확인 `B2C_1A_GoogleSecret`합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="a159e-159">확장 정책에서 클레임 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="a159e-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="a159e-160">Google + 계정을 사용 하 여 사용자가 toosign에서 원하는 클레임 공급자로 toodefine Google + 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="a159e-161">즉, Azure AD B2C와 통신 하는 끝점 toospecify를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="a159e-162">hello 끝점은 특정 사용자가 인증 하는 Azure AD B2C tooverify에서 사용 되는 클레임 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="a159e-163">확장 정책 파일에서 `<ClaimsProvider>` 노드를 추가하여 Google+ 계정을 클레임 공급자로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="a159e-164">작업 디렉터리부터 hello 확장명 정책 파일 (TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="a159e-165">XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="a159e-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="a159e-166">Hello `<ClaimsProviders>` 섹션</span><span class="sxs-lookup"><span data-stu-id="a159e-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="a159e-167">Hello hello 아래 XML 조각 다음 추가 `ClaimsProviders` 요소 및 바꾸기 `client_id` Google + 계정 응용 프로그램 클라이언트 ID로 hello 파일 저장 하기 전에 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="a159e-168">Hello Google + 계정 클레임 공급자 tooSign를 등록 하거나 사용자의 여행 로그인</span><span class="sxs-lookup"><span data-stu-id="a159e-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="a159e-169">hello id 공급자 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="a159e-170">그러나, hello 로그-up/로그인 화면 중에서 가능 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="a159e-171">Hello Google + 계정 id 공급자 tooyour 사용자 추가 `SignUpOrSignIn` 사용자 여행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="a159e-172">toomake 기존 템플릿 사용자 여행 중복 만듭니다 사용할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="a159e-173">Hello Google + 계정 id 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="a159e-174">Hello를 복사한 경우 `<UserJourneys>` 요소 (TrustFrameworkExtensions.xml) 정책 toohello 확장 파일의 기본 파일 로부터 toothis 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="a159e-175">Hello 정책 (예를 들어 TrustFrameworkBase.xml)의 기본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="a159e-176">Hello `<UserJourneys>` 의 요소와 복사 hello 전체 내용을 `<UserJourneys>` 노드.</span><span class="sxs-lookup"><span data-stu-id="a159e-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="a159e-177">Hello 확장 파일 (예를 들어 TrustFrameworkExtensions.xml)를 열고 hello `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="a159e-178">존재 하지 않으면 hello 요소 하나를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="a159e-179">전체 내용을 hello `<UserJournesy>` hello의 자식으로 복사한 노드 `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="a159e-180">디스플레이 hello 단추</span><span class="sxs-lookup"><span data-stu-id="a159e-180">Display hello button</span></span>
<span data-ttu-id="a159e-181">hello `<ClaimsProviderSelections>` 요소 hello 클레임 공급자 선택 옵션 목록 및 해당 순서를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="a159e-182">`<ClaimsProviderSelection>`요소는 로그-up/로그인 페이지에 유사한 tooan identity provider 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="a159e-183">추가 하는 경우는 `<ClaimsProviderSelection>` Google + 계정에 대 한 요소, 사용자 hello 페이지에 처음 삽입 새 단추 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="a159e-184">tooadd이이 요소:</span><span class="sxs-lookup"><span data-stu-id="a159e-184">tooadd this element:</span></span>

1.  <span data-ttu-id="a159e-185">Hello `<UserJourney>` 포함 된 노드 `Id="SignUpOrSignIn"` 복사한 hello 사용자 여정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="a159e-186">Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="a159e-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="a159e-187">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="a159e-188">링크 hello 단추 tooan 동작</span><span class="sxs-lookup"><span data-stu-id="a159e-188">Link hello button tooan action</span></span>
<span data-ttu-id="a159e-189">Toolink 필요한 위치에 있는 단추를가지고 그 tooan 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="a159e-190">hello 동작이 경우 계정 tooreceive Google +와 Azure AD B2C toocommunicate에 대 한 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="a159e-191">Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.</span><span class="sxs-lookup"><span data-stu-id="a159e-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="a159e-192">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="a159e-193">Hello 확인 `Id` 의과 같은 값인 hello에 `TargetClaimsExchangeId` hello 앞 섹션에서</span><span class="sxs-lookup"><span data-stu-id="a159e-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="a159e-194">확인 `TechnicalProfileReferenceId` 이전 (Google OAUTH)를 만든 toohello 기술 프로필 ID가 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="a159e-195">Hello 정책 tooyour 테 넌 트에 업로드</span><span class="sxs-lookup"><span data-stu-id="a159e-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="a159e-196">Hello에 [Azure 포털](https://portal.azure.com), hello를 전환 [Azure AD B2C 테 넌 트의 상황에 맞는](active-directory-b2c-navigate-to-b2c-context.md), 및 열기 hello **Azure AD B2C** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="a159e-197">**ID 경험 프레임워크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="a159e-198">열기 hello **모든 정책** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="a159e-199">**정책 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="a159e-200">확인 **있으면 hello 정책 덮어쓰기** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="a159e-201">**업로드** TrustFrameworkExtensions.xml hello 유효성 검사가 발생 하지 않도록 하 고</span><span class="sxs-lookup"><span data-stu-id="a159e-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="a159e-202">지금 실행에 사용 하 여 hello 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="a159e-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="a159e-203">열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="a159e-204">**지금 실행** hello 테 넌 트에 응용 프로그램이 하나 이상 toobe 미리 등록 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="a159e-205">toolearn tooregister 응용 프로그램을 확인 하려면 어떻게 해야 Azure AD B2C hello [시작](active-directory-b2c-get-started.md) 문서 또는 hello [응용 프로그램 등록](active-directory-b2c-app-registration.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a159e-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="a159e-206">열기 **B2C_1A_signup_signin**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="a159e-207">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="a159e-208">Google + 계정을 사용 하 여 수 toosign 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="a159e-209">[선택 사항] Hello Google + 계정 클레임 공급자 tooProfile 편집 사용자 여행 등록</span><span class="sxs-lookup"><span data-stu-id="a159e-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="a159e-210">좋습니다 tooadd hello Google + 계정 id 공급자도 tooyour 사용자 `ProfileEdit` 사용자 여행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="a159e-211">toomake 마지막 두 단계 hello 반복 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="a159e-212">디스플레이 hello 단추</span><span class="sxs-lookup"><span data-stu-id="a159e-212">Display hello button</span></span>
1.  <span data-ttu-id="a159e-213">정책 (예를 들어 TrustFrameworkExtensions.xml) hello 확장 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="a159e-214">Hello `<UserJourney>` 포함 된 노드 `Id="ProfileEdit"` 복사한 hello 사용자 여정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="a159e-215">Hello 찾을 `<OrchestrationStep>` 포함 된 노드`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="a159e-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="a159e-216">`<ClaimsProviderSelections>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="a159e-217">링크 hello 단추 tooan 동작</span><span class="sxs-lookup"><span data-stu-id="a159e-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="a159e-218">Hello `<OrchestrationStep>` 포함 된 `Order="2"` hello에 `<UserJourney>` 노드.</span><span class="sxs-lookup"><span data-stu-id="a159e-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="a159e-219">`<ClaimsExchanges>` 노드 아래에서 다음 XML 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="a159e-220">지금 실행에 사용 하 여 hello 사용자 지정 프로필 편집 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="a159e-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="a159e-221">열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="a159e-222">열기 **B2C_1A_ProfileEdit**를 업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="a159e-223">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="a159e-224">Google + 계정을 사용 하 여 수 toosign 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="a159e-225">Hello 완성 된 정책 파일을 다운로드</span><span class="sxs-lookup"><span data-stu-id="a159e-225">Download hello complete policy files</span></span>
<span data-ttu-id="a159e-226">선택 사항: 권장 사용자 고유의 사용자 지정 정책 파일을 사용 하 여 이러한 샘플 파일을 사용 하는 대신 안내 사용자 지정 정책을 사용 하 여 시작 하는 hello를 완료 한 후 시나리오를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a159e-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="a159e-227">참조할 샘플 정책 파일</span><span class="sxs-lookup"><span data-stu-id="a159e-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
