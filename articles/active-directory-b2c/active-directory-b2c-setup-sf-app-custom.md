---
title: "Azure Active Directory B2C: 사용자 지정 정책을 사용하여 Salesforce SAML 공급자 추가 | Microsoft Docs"
description: "Azure Active Directory B2C 사용자 지정 정책을 만들고 관리하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="90d0a-103">Azure Active Directory B2C: SAML을 통해 Salesforce 계정을 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="90d0a-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="90d0a-104">이 문서에서는 [사용자 지정 정책](active-directory-b2c-overview-custom.md)을 사용하여 특정 Salesforce 조직의 사용자가 로그인할 수 있도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90d0a-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="90d0a-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="90d0a-106">Azure AD B2C 설정</span><span class="sxs-lookup"><span data-stu-id="90d0a-106">Azure AD B2C setup</span></span>

<span data-ttu-id="90d0a-107">Azure AD B2C(Azure Active Directory B2C)에서 [사용자 지정 정책을 사용하여 시작](active-directory-b2c-get-started-custom.md)하는 방법을 설명하는 단계를 모두 완료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="90d0a-108">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-108">These include:</span></span>

* <span data-ttu-id="90d0a-109">Azure AD B2C 테넌트 만들기</span><span class="sxs-lookup"><span data-stu-id="90d0a-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="90d0a-110">Azure AD B2C 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="90d0a-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="90d0a-111">두 개의 정책 엔진 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="90d0a-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="90d0a-112">키 설정</span><span class="sxs-lookup"><span data-stu-id="90d0a-112">Set up keys.</span></span>
* <span data-ttu-id="90d0a-113">시작 팩 설정</span><span class="sxs-lookup"><span data-stu-id="90d0a-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="90d0a-114">Salesforce 설정</span><span class="sxs-lookup"><span data-stu-id="90d0a-114">Salesforce setup</span></span>

<span data-ttu-id="90d0a-115">이 문서에서는 다음을 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="90d0a-116">Salesforce 계정 등록.</span><span class="sxs-lookup"><span data-stu-id="90d0a-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="90d0a-117">[Developer Edition 평가판 계정](https://developer.salesforce.com/signup)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="90d0a-118">Salesforce 조직에 [내 도메인을 설정](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="90d0a-119">사용자가 페더레이션할 수 있도록 Salesforce 설정</span><span class="sxs-lookup"><span data-stu-id="90d0a-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="90d0a-120">Azure AD B2C가 Salesforce와 통신하도록 지원하려면 Salesforce 메타데이터 URL을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="90d0a-121">Salesforce를 ID 공급자로 설정</span><span class="sxs-lookup"><span data-stu-id="90d0a-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="90d0a-122">이 문서에서는 [Salesforce Lightning 환경](https://developer.salesforce.com/page/Lightning_Experience_FAQ)을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="90d0a-123">[Salesforce에 로그인](https://login.salesforce.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="90d0a-124">왼쪽 메뉴의 **설정** 아래에서 **ID**를 확장하고 **ID 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="90d0a-125">**ID 공급자 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="90d0a-126">**인증서 선택** 아래에서 Salesforce가 Azure AD B2C와 통신할 때 사용할 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="90d0a-127">(기본 인증서를 사용할 수 있습니다.) **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="90d0a-128">Salesforce에서 연결된 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="90d0a-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="90d0a-129">**ID 공급자** 페이지에서 **서비스 공급자**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="90d0a-130">**Service Providers are now created via Connected Apps. Click here.**(서비스 공급자가 연결된 앱을 통해 생성됩니다. 여기를 클릭하세요.)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="90d0a-131">**기본 정보** 아래에서 연결된 앱에 대한 필수 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="90d0a-132">**Web App 설정**아래에서 **SAML 설정** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="90d0a-133">**엔터티 ID** 필드에 다음 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="90d0a-134">`tenantName`에 대한 값을 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="90d0a-135">**ACS URL** 필드에 다음 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="90d0a-136">`tenantName`에 대한 값을 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="90d0a-137">다른 모든 설정에 대한 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="90d0a-138">목록 아래쪽으로 스크롤한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="90d0a-139">메타데이터 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="90d0a-139">Get the metadata URL</span></span>

1. <span data-ttu-id="90d0a-140">연결된 앱의 개요 페이지에서 **관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="90d0a-141">**메타데이터 검색 끝점** 값을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="90d0a-142">이 문서의 뒷부분에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="90d0a-143">Salesforce 사용자가 페더레이션하도록 설정</span><span class="sxs-lookup"><span data-stu-id="90d0a-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="90d0a-144">연결된 앱의 **관리** 페이지에서 **프로필**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="90d0a-145">**프로필 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="90d0a-146">Azure AD B2C와 페더레이션하려는 프로필(또는 사용자 그룹)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="90d0a-147">시스템 관리자 권한으로 Salesforce 계정을 사용하여 페더레이션할 수 있도록 **시스템 관리자** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="90d0a-148">Azure AD B2C에 대한 서명 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="90d0a-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="90d0a-149">Azure AD B2C는 Salesforce에 전송되는 요청에 서명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="90d0a-150">서명 인증서를 생성하려면 Azure PowerShell을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="90d0a-151">맨 위 두 줄에서 테넌트 이름 및 암호를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="90d0a-152">Azure AD B2C에 SAML 서명 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="90d0a-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="90d0a-153">서명 인증서를 Azure AD B2C 테넌트에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="90d0a-154">Azure AD B2C 테넌트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="90d0a-155">**설정** > **ID 환경 프레임워크** > **정책 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="90d0a-156">**+추가**를 클릭한 다음</span><span class="sxs-lookup"><span data-stu-id="90d0a-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="90d0a-157">**옵션** > **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="90d0a-158">**이름**을 입력합니다(예: SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="90d0a-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="90d0a-159">키의 이름에 *B2C_1A_* 접두사가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="90d0a-160">인증서를 선택하려면 **업로드 파일 제어**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="90d0a-161">PowerShell 스크립트에서 설정한 인증서 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="90d0a-162">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-162">Click **Create**.</span></span>
4. <span data-ttu-id="90d0a-163">키를 만들었는지 확인합니다(예: B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="90d0a-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="90d0a-164">전체 이름을 기록해둡니다(*B2C_1A_*를 포함).</span><span class="sxs-lookup"><span data-stu-id="90d0a-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="90d0a-165">정책에서 나중에 이 키를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="90d0a-166">기본 정책에서 Salesforce SAML 클레임 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="90d0a-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="90d0a-167">사용자가 Salesforce를 사용하여 로그인할 수 있도록 Salesforce를 클레임 공급자로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="90d0a-168">즉, Azure AD B2C가 통신할 끝점을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="90d0a-169">끝점은 Azure AD B2C에서 사용하는 일련의 *클레임*을 *제공*하여 특정 사용자가 인증했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="90d0a-170">그렇게 하려면 정책의 확장 파일에서 Salesforce에 대한 `<ClaimsProvider>`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="90d0a-171">작업 디렉터리에서 확장 파일(TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="90d0a-172">`<ClaimsProviders>` 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="90d0a-173">존재하지 않는 경우 루트 노드에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="90d0a-174">새 `<ClaimsProvider>`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="90d0a-175">`<ClaimsProvider>` 노드 아래에서:</span><span class="sxs-lookup"><span data-stu-id="90d0a-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="90d0a-176">`<Domain>` 값을 다른 ID 공급자와 `<ClaimsProvider>`를 구분하는 데 사용할 수 있는 고유한 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="90d0a-177">`<DisplayName>` 값을 클레임 공급자의 표시 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="90d0a-178">이 값은 현재 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="90d0a-179">기술 프로필 업데이트</span><span class="sxs-lookup"><span data-stu-id="90d0a-179">Update the technical profile</span></span>

<span data-ttu-id="90d0a-180">Salesforce에서 SAML 토큰을 가져오려면 Azure AD B2C에서 Azure AD(Azure Active Directory)와 통신하는 데 사용하는 프로토콜을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="90d0a-181">`<ClaimsProvider>`의 `<TechnicalProfile>` 요소에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="90d0a-182">`<TechnicalProfile>` 노드의 ID를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="90d0a-183">이 ID는 정책의 다른 부분에서 이 기술 프로필을 참조하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="90d0a-184">`<DisplayName>` 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="90d0a-185">이 값은 로그인 페이지의 로그인 단추에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="90d0a-186">`<Description>` 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="90d0a-187">Salesforce에서는 SAML 2.0 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="90d0a-188">`<Protocol>`에 대한 값이 **SAML2**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="90d0a-189">이전 XML에서 `<Metadata>` 섹션을 업데이트하여 특정 Salesforce 계정의 설정을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="90d0a-190">XML에서 메타데이터 값을 다음과 같이 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="90d0a-191">`<Item Key="PartnerEntity">` 값을 앞에서 복사한 Salesforce 메타데이터 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="90d0a-192">다음과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="90d0a-193">`<CryptographicKeys>` 섹션에서 `StorageReferenceId`의 두 인스턴스 값을 모두 서명 인증서(예: B2C_1A_SAMLSigningCert)의 키 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="90d0a-194">확인을 위한 확장 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="90d0a-194">Upload the extension file for verification</span></span>

<span data-ttu-id="90d0a-195">이제 Azure AD B2C에서 Salesforce와 통신하는 방법을 알 수 있도록 정책이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="90d0a-196">정책의 확장 파일을 업로드하여 지금까지 문제가 발생하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="90d0a-197">정책의 확장 파일을 업로드하려면:</span><span class="sxs-lookup"><span data-stu-id="90d0a-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="90d0a-198">Azure AD B2C 테넌트에서 **모든 정책** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="90d0a-199">**정책이 있는 경우 덮어쓰기** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="90d0a-200">확장 파일(TrustFrameworkExtensions.xml)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="90d0a-201">유효성 검사를 실패하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="90d0a-202">사용자 경험에 Salesforce SAML 클레임 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="90d0a-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="90d0a-203">다음으로 사용자 경험 중 하나에 Salesforce SAML ID 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="90d0a-204">이 시점에서 ID 공급자가 설정되었지만 등록 또는 로그인 페이지에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="90d0a-205">ID 공급자를 로그인 페이지에 추가하려면 먼저 기존 템플릿 사용자 경험의 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="90d0a-206">그런 다음 Azure AD ID 공급자를 포함하도록 템플릿을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="90d0a-207">정책의 기본 파일(예: TrustFrameworkBase.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="90d0a-208">Id=”SignUpOrSignIn”을 포함하여 `<UserJourneys>` 요소를 찾고 전체 `<UserJourney>` 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="90d0a-209">확장 파일(예: TrustFrameworkExtensions.xml)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="90d0a-210">`<UserJourneys>` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="90d0a-211">요소가 존재하지 않는 경우 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="90d0a-212">복사한 전체 `<UserJourney>`을 `<UserJourneys>` 요소의 자식으로 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="90d0a-213">새 `<UserJourney>`의 ID 이름을 바꿉니다(예: SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="90d0a-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="90d0a-214">ID 공급자 단추 표시</span><span class="sxs-lookup"><span data-stu-id="90d0a-214">Display the identity provider button</span></span>

<span data-ttu-id="90d0a-215">`<ClaimsProviderSelection>` 요소는 등록 또는 로그인 페이지에서 ID 공급자 단추를 사용하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="90d0a-216">Salesforce에 `<ClaimsProviderSelection>` 요소를 추가하여 사용자가 이 페이지로 이동하면 새 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="90d0a-217">ID 공급자 단추를 표시하려면:</span><span class="sxs-lookup"><span data-stu-id="90d0a-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="90d0a-218">사용자가 만든 `<UserJourney>`에서 `<OrchestrationStep>`와 `Order="1"`을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="90d0a-219">다음 XML을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="90d0a-220">`TargetClaimsExchangeId`을 논리값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="90d0a-221">다른 값과 동일한 규칙을 사용하는 것이 좋습니다(예: *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="90d0a-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="90d0a-222">작업에 ID 공급자 단추 연결</span><span class="sxs-lookup"><span data-stu-id="90d0a-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="90d0a-223">이제 ID 공급자 단추를 만들었으므로 작업에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="90d0a-224">이 경우에 작업은 Azure AD B2C에서 Salesforce와 통신하여 SAML 토큰을 수신할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="90d0a-225">이렇게 하려면 Salesforce SAML 클레임 공급자의 기술 프로필을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="90d0a-226">`<UserJourney>` 노드에서 `<OrchestrationStep>`와 `Order="2"`을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="90d0a-227">다음 XML을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="90d0a-228">`Id`을 `TargetClaimsExchangeId`에 사용한 동일한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="90d0a-229">`TechnicalProfileReferenceId`를 이전에 만든 기술 프로필의 `Id`로 업데이트합니다(예: ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="90d0a-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="90d0a-230">업데이트된 확장 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="90d0a-230">Upload the updated extension file</span></span>

<span data-ttu-id="90d0a-231">확장 파일을 수정하는 작업을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-231">You are done modifying the extension file.</span></span> <span data-ttu-id="90d0a-232">이 파일을 저장하고 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-232">Save and upload this file.</span></span> <span data-ttu-id="90d0a-233">모든 유효성 검사에 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="90d0a-234">신뢰 당사자 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="90d0a-234">Update the relying party file</span></span>

<span data-ttu-id="90d0a-235">다음으로, 만든 사용자 경험을 시작할 RP(신뢰 당사자) 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="90d0a-236">작업 디렉터리에서 SignUpOrSignIn.xml의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="90d0a-237">그런 다음 이름을 바꿉니다(예: SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="90d0a-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="90d0a-238">새 파일을 열고 `<TrustFrameworkPolicy>`의 `PolicyId` 특성을 고유한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="90d0a-239">이는 정책의 이름(예: SignUpOrSignInWithAAD)입니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="90d0a-240">`<DefaultUserJourney>`에서 `ReferenceId` 특성을 수정하여 만든 새 사용자 경험의 `Id`와 일치시킵니다(예: SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="90d0a-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="90d0a-241">변경 내용을 저장하고 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="90d0a-242">테스트 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="90d0a-242">Test and troubleshoot</span></span>

<span data-ttu-id="90d0a-243">Azure Portal에서 방금 업로드한 사용자 지정 정책을 테스트하려면 정책 블레이드로 이동하고 **지금 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="90d0a-244">실패한 경우 [사용자 지정 정책 문제 해결](active-directory-b2c-troubleshoot-custom.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90d0a-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90d0a-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90d0a-245">Next steps</span></span>

<span data-ttu-id="90d0a-246">[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)에 대한 피드백을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90d0a-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
