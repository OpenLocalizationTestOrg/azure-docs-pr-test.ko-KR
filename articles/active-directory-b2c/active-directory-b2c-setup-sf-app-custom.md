---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 Salesforce SAML 공급자 추가 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 toocreate 및 Azure Active Directory B2C 사용자 지정 정책을 관리 합니다."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="2fe74-103">Azure Active Directory B2C: SAML을 통해 Salesforce 계정을 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="2fe74-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="2fe74-104">이 문서에서는 어떻게 toouse [사용자 지정 정책을](active-directory-b2c-overview-custom.md) tooset 로그인 특정 Salesforce 조직에서 사용자가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fe74-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2fe74-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="2fe74-106">Azure AD B2C 설정</span><span class="sxs-lookup"><span data-stu-id="2fe74-106">Azure AD B2C setup</span></span>

<span data-ttu-id="2fe74-107">모든 너무 방법을 보여 주는 hello 단계를 완료 했는지 확인 하십시오.[사용자 지정 정책 시작](active-directory-b2c-get-started-custom.md) Azure Active Directory B2C에 (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="2fe74-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="2fe74-108">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-108">These include:</span></span>

* <span data-ttu-id="2fe74-109">Azure AD B2C 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="2fe74-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="2fe74-110">Azure AD B2C 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2fe74-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="2fe74-111">두 개의 정책 엔진 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="2fe74-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="2fe74-112">키 설정</span><span class="sxs-lookup"><span data-stu-id="2fe74-112">Set up keys.</span></span>
* <span data-ttu-id="2fe74-113">Hello 스타터 팩을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="2fe74-114">Salesforce 설정</span><span class="sxs-lookup"><span data-stu-id="2fe74-114">Salesforce setup</span></span>

<span data-ttu-id="2fe74-115">이 문서에서는 hello 다음 이미 추가한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="2fe74-116">Salesforce 계정 등록.</span><span class="sxs-lookup"><span data-stu-id="2fe74-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="2fe74-117">[Developer Edition 평가판 계정](https://developer.salesforce.com/signup)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="2fe74-118">Salesforce 조직에 [내 도메인을 설정](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="2fe74-119">사용자가 페더레이션할 수 있도록 Salesforce 설정</span><span class="sxs-lookup"><span data-stu-id="2fe74-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="2fe74-120">Salesforce와 toohelp Azure AD B2C 통신, tooget hello Salesforce 메타 데이터 URL이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="2fe74-121">Salesforce를 ID 공급자로 설정</span><span class="sxs-lookup"><span data-stu-id="2fe74-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="2fe74-122">이 문서에서는 [Salesforce Lightning 환경](https://developer.salesforce.com/page/Lightning_Experience_FAQ)을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="2fe74-123">[TooSalesforce 로그인](https://login.salesforce.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="2fe74-124">Hello 왼쪽 메뉴 아래에서 **설정**를 확장 하 고 **Identity**, 클릭 하 고 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="2fe74-125">**ID 공급자 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="2fe74-126">아래 **선택 hello 인증서**선택, Azure AD B2C와 Salesforce toouse toocommunicate hello 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="2fe74-127">(Hello 기본 인증서를 사용할 수 있습니다.) **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="2fe74-128">Salesforce에서 연결된 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2fe74-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="2fe74-129">Hello에 **Id 공급자** 페이지에서 이동 너무**서비스 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="2fe74-130">**Service Providers are now created via Connected Apps. Click here.**(서비스 공급자가 연결된 앱을 통해 생성됩니다. 여기를 클릭하세요.)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="2fe74-131">아래 **기본 정보**, 연결 된 앱에 대 한 hello 필요한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="2fe74-132">아래 **웹 앱 설정을**선택, hello **SAML을 사용 하도록 설정** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="2fe74-133">Hello에 **엔터티 ID** 필드 hello url을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="2fe74-134">에 대 한 hello 값 바꾸어야 `tenantName`합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="2fe74-135">Hello에 **ACS URL** 필드 hello url을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="2fe74-136">에 대 한 hello 값 바꾸어야 `tenantName`합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="2fe74-137">다른 모든 설정에 대 한 hello 기본값 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="2fe74-138">Hello 목록의 toohello 아래쪽 스크롤한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="2fe74-139">Hello 메타 데이터 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="2fe74-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="2fe74-140">연결 된 응용 프로그램의 hello 개요 페이지에서 클릭 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="2fe74-141">Hello 값을 복사 **메타 데이터 검색 끝점**를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="2fe74-142">이 문서의 뒷부분에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="2fe74-143">Salesforce 사용자 toofederate 설정</span><span class="sxs-lookup"><span data-stu-id="2fe74-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="2fe74-144">Hello에 **관리** 페이지 연결 된 응용 프로그램의 이동 너무**프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="2fe74-145">**프로필 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="2fe74-146">Hello 프로필 (또는 사용자 그룹을) 선택와 Azure AD B2C toofederate 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="2fe74-147">시스템 관리자로 hello 선택 **시스템 관리자에 게** 확인란 Salesforce 계정을 사용 하 여 페더레이션 할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="2fe74-148">Azure AD B2C에 대한 서명 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="2fe74-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="2fe74-149">요청은 Azure AD B2C 서명한 tooSalesforce 필요 toobe를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="2fe74-150">toogenerate 서명 인증서를 Azure PowerShell을 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="2fe74-151">Hello 상위 두 줄에 hello 테 넌 트 이름 및 암호를 업데이트 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="2fe74-152">Hello SAML 서명 인증서 tooAzure AD B2C 추가</span><span class="sxs-lookup"><span data-stu-id="2fe74-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="2fe74-153">서명 인증서 tooyour Azure AD B2C 테 넌 트 hello를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="2fe74-154">Tooyour Azure AD B2C 테 넌 트를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="2fe74-155">**설정** > **ID 환경 프레임워크** > **정책 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="2fe74-156">**+추가**를 클릭한 다음</span><span class="sxs-lookup"><span data-stu-id="2fe74-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="2fe74-157">**옵션** > **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="2fe74-158">**이름**을 입력합니다(예: SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="2fe74-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="2fe74-159">hello 접두사 *B2C_1A_* 키의 toohello 이름을 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="2fe74-160">tooselect 인증서를 선택 **업로드 파일 컨트롤**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="2fe74-161">Hello PowerShell 스크립트에서 설정한 hello 인증서의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="2fe74-162">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-162">Click **Create**.</span></span>
4. <span data-ttu-id="2fe74-163">키를 만들었는지 확인합니다(예: B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="2fe74-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="2fe74-164">전체 이름 hello 기록해 둡니다 (포함 하 여 *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="2fe74-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="2fe74-165">Hello 정책의 뒷부분에 나오는 toothis 키를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="2fe74-166">기본 정책에서 hello Salesforce SAML 클레임 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="2fe74-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="2fe74-167">Salesforce를 사용 하 여 사용자가 로그인 할 수 있도록 Salesforce toodefine를 클레임 공급자로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="2fe74-168">즉, Azure AD B2C 통신할 toospecify hello 끝점을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="2fe74-169">hello 끝점은 *제공* 집합이 *클레임* Azure AD B2C tooverify 특정 사용자가 자신을 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="2fe74-170">toodo이 추가 `<ClaimsProvider>` 정책 hello 확장 파일에서 Salesforce에 대 한:</span><span class="sxs-lookup"><span data-stu-id="2fe74-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="2fe74-171">작업 디렉터리에서 hello 확장 파일 (TrustFrameworkExtensions.xml)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="2fe74-172">Hello `<ClaimsProviders>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="2fe74-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="2fe74-173">존재 하지 않는 경우 hello 루트 노드에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="2fe74-174">새 `<ClaimsProvider>`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

<span data-ttu-id="2fe74-175">Hello에서 `<ClaimsProvider>` 노드:</span><span class="sxs-lookup"><span data-stu-id="2fe74-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="2fe74-176">Hello 값에 대 한 변경 `<Domain>` 구별 하는 고유한 값 tooa `<ClaimsProvider>` 기타 id 공급자에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="2fe74-177">에 대 한 hello 시간 `<DisplayName>` hello에 대 한 tooa 표시 이름 클레임 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="2fe74-178">이 값은 현재 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="2fe74-179">Hello 기술 프로필 업데이트</span><span class="sxs-lookup"><span data-stu-id="2fe74-179">Update hello technical profile</span></span>

<span data-ttu-id="2fe74-180">tooget Salesforce에서 SAML 토큰을 Azure AD B2C ´ ֲ toocommunicate Azure Active Directory (Azure AD)와 hello 프로토콜을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="2fe74-181">Hello에서 이렇게 `<TechnicalProfile>` 요소의 `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="2fe74-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="2fe74-182">업데이트의 hello hello ID `<TechnicalProfile>` 노드.</span><span class="sxs-lookup"><span data-stu-id="2fe74-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="2fe74-183">이 ID가 사용 되는 toorefer toothis hello 정책의 다른 부분과에서 기술 프로필.</span><span class="sxs-lookup"><span data-stu-id="2fe74-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="2fe74-184">에 대 한 hello 시간 `<DisplayName>`합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="2fe74-185">이 값은 로그인 페이지에 hello 로그인 단추에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="2fe74-186">에 대 한 hello 시간 `<Description>`합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="2fe74-187">Salesforce는 hello SAML 2.0 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="2fe74-188">에 대 한 해당 hello 값 확인 `<Protocol>` 은 **SAML2**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="2fe74-189">업데이트 hello `<Metadata>` hello 특정 Salesforce 계정에 대 한 XML tooreflect hello 설정을 앞의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="2fe74-190">XML hello에서 hello 메타 데이터 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="2fe74-191">Hello 값을 업데이트 `<Item Key="PartnerEntity">` 앞에서 복사한 hello Salesforce 메타 데이터 URL로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="2fe74-192">형식에 따라 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="2fe74-193">Hello에 `<CryptographicKeys>` 섹션의 두 인스턴스에 대 한 업데이트 hello 값 `StorageReferenceId` toohello 이름 서명 인증서 (예를 들어 B2C_1A_SAMLSigningCert)의 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="2fe74-194">확인에 대 한 hello 확장 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="2fe74-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="2fe74-195">정책에는 이제 Azure AD B2C 알 수 있도록 구성 되었습니다 어떻게 salesforce toocommunicate 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="2fe74-196">정책 되지 않게 문제 지금까지 tooverify hello 확장 파일을 업로드 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2fe74-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="2fe74-197">정책 tooupload hello 확장 파일:</span><span class="sxs-lookup"><span data-stu-id="2fe74-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="2fe74-198">Azure AD B2C 테 넌 트에 toohello 이동 **모든 정책** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="2fe74-199">선택 hello **있으면 hello 정책 덮어쓰기** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="2fe74-200">Hello 확장 파일 (TrustFrameworkExtensions.xml)를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="2fe74-201">유효성 검사를 실패하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="2fe74-202">Salesforce SAML 클레임 공급자의 tooa 사용자 여행 hello 등록</span><span class="sxs-lookup"><span data-stu-id="2fe74-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="2fe74-203">다음으로 사용자 친구의 Salesforce SAML identity provider tooone hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="2fe74-204">이 시점에서 hello id 공급자 설정 되어 있지만 hello 사용자 등록 또는 로그인 페이지에서 사용할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="2fe74-205">먼저 tooadd hello id 공급자 tooa 로그인 페이지에서 기존 템플릿 사용자 여행의 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="2fe74-206">그런 다음 hello Azure AD id 공급자를 포함 하므로 hello 템플릿을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="2fe74-207">Hello 정책 (예를 들어 TrustFrameworkBase.xml)의 기본 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="2fe74-208">Hello `<UserJourneys>` 요소 및 전체 복사 hello `<UserJourney>` , 값 = "SignUpOrSignIn" Id를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="2fe74-209">Hello 확장 파일 (예를 들어 TrustFrameworkExtensions.xml)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="2fe74-210">Hello `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="2fe74-211">Hello 요소가 존재 하지 않는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="2fe74-212">붙여넣기 hello 전체 복사 `<UserJourney>` hello의 자식으로 `<UserJourneys>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="2fe74-213">새 hello의 hello ID 이름 바꾸기 `<UserJourney>` (예를 들어 SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="2fe74-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="2fe74-214">디스플레이 hello identity provider 단추</span><span class="sxs-lookup"><span data-stu-id="2fe74-214">Display hello identity provider button</span></span>

<span data-ttu-id="2fe74-215">hello `<ClaimsProviderSelection>` 요소는 등록 또는 로그인 페이지에 유사한 tooan identity provider 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="2fe74-216">추가 하 여 프로그램 `<ClaimsProviderSelection>` toothis 페이지 이동할 때 Salesforce에 대 한 요소를 새 단추가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="2fe74-217">toodisplay hello identity provider 단추:</span><span class="sxs-lookup"><span data-stu-id="2fe74-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="2fe74-218">Hello에 `<UserJourney>` hello, 만든 `<OrchestrationStep>` 와 `Order="1"`합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="2fe74-219">다음과 같은 XML hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="2fe74-220">설정 `TargetClaimsExchangeId` tooa 논리 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="2fe74-221">다음 hello 동일한 것이 좋습니다 다른 사용자와 규칙 (예를 들어  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="2fe74-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="2fe74-222">링크 hello identity provider 단추 tooan 동작</span><span class="sxs-lookup"><span data-stu-id="2fe74-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="2fe74-223">Identity provider 단추 준비에서를 tooan 작업을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="2fe74-224">이 경우 Azure AD B2C toocommunicate와 Salesforce tooreceive SAML 토큰에 대 한 hello 동작이입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="2fe74-225">수행할 수 있습니다이 Salesforce SAML에 대 한 기술 hello 프로필에 연결 하 여 클레임 공급자.</span><span class="sxs-lookup"><span data-stu-id="2fe74-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="2fe74-226">Hello에 `<UserJourney>` 노드, 찾기 hello `<OrchestrationStep>` 와 `Order="2"`합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="2fe74-227">다음과 같은 XML hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="2fe74-228">업데이트 `Id` toohello 동일한 값에 대 한 이전 사용 `TargetClaimsExchangeId`합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="2fe74-229">업데이트 `TechnicalProfileReferenceId` toohello `Id` hello 기술의 프로필 앞에서 만든 (예를 들어 ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="2fe74-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="2fe74-230">Hello 업데이트 된 확장 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="2fe74-230">Upload hello updated extension file</span></span>

<span data-ttu-id="2fe74-231">Hello 확장 파일을 수정 하 고 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="2fe74-232">이 파일을 저장하고 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-232">Save and upload this file.</span></span> <span data-ttu-id="2fe74-233">모든 유효성 검사에 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="2fe74-234">Hello 신뢰 당사자 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="2fe74-234">Update hello relying party file</span></span>

<span data-ttu-id="2fe74-235">다음으로 만든 hello 사용자 작업을 시작 하는 hello 신뢰 하는 파티 (RP) 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="2fe74-236">작업 디렉터리에서 SignUpOrSignIn.xml의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="2fe74-237">그런 다음 이름을 바꿉니다(예: SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="2fe74-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="2fe74-238">열기 hello 새 파일 및 업데이트 hello `PolicyId` 특성 `<TrustFrameworkPolicy>` 고유 값으로.</span><span class="sxs-lookup"><span data-stu-id="2fe74-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="2fe74-239">정책 (예를 들어 SignUpOrSignInWithAAD) hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="2fe74-240">Hello 수정 `ReferenceId` 특성 `<DefaultUserJourney>` toomatch hello `Id` hello 새 사용자의 여행 (예: SignUpOrSignUsingContoso) 생성의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="2fe74-241">변경 내용을 저장 하 고 hello 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="2fe74-242">테스트 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2fe74-242">Test and troubleshoot</span></span>

<span data-ttu-id="2fe74-243">hello Azure 포털에서에서 방금 업로드 tootest hello 사용자 지정 정책 toohello 정책 블레이드에서 이동한 다음 클릭 **지금 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="2fe74-244">실패한 경우 [사용자 지정 정책 문제 해결](active-directory-b2c-troubleshoot-custom.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fe74-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fe74-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2fe74-245">Next steps</span></span>

<span data-ttu-id="2fe74-246">피드백을 너무 제공[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2fe74-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
