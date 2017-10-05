---
title: "Azure Active Directory B2C: 사용자 고유의 특성을 사용자 지정 정책에 추가하고 프로필 편집에 사용 | Microsoft Docs"
description: "확장 속성, 사용자 지정 특성을 사용하고 사용자 인터페이스에 포함하는 방법에 대한 연습"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 67c9f6eca18e2dd77e00b8bc8c7bcc546ea3936e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="a57e5-103">Azure Active Directory B2C: 사용자 지정 프로필 편집 정책에서 사용자 지정 특성을 만들고 사용</span><span class="sxs-lookup"><span data-stu-id="a57e5-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="a57e5-104">이 문서에서는 Azure AD B2C 디렉터리에 사용자 지정 특성을 만들고 이 새로운 특성을 프로필 편집 사용자 경험에서 사용자 지정 클레임으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in the profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a57e5-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a57e5-105">Prerequisites</span></span>

<span data-ttu-id="a57e5-106">[사용자 지정 정책을 사용하여 시작](active-directory-b2c-get-started-custom.md) 문서의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-106">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-to-collect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="a57e5-107">사용자 지정 특성을 사용하여 사용자 지정 정책을 사용하는 Azure Active Directory B2C에서 고객에 대한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-107">Use custom attributes to collect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="a57e5-108">Azure Active Directory(Azure AD) B2C 디렉터리에는 지정된 이름, 성, 도시, 우편 번호, userPrincipalName의 특성 집합이 함께 제공됩니다.  주로 고유한 특성을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need to create your own attributes.</span></span>  <span data-ttu-id="a57e5-109">예:</span><span class="sxs-lookup"><span data-stu-id="a57e5-109">For example:</span></span>
* <span data-ttu-id="a57e5-110">고객 대면 응용 프로그램은 "LoyaltyNumber"와 같은 특성을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-110">A customer-facing application needs to persist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="a57e5-111">ID 공급자는 "uniqueUserGUID"처럼 저장해야 하는 고유한 사용자 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="a57e5-112">사용자 지정 사용자 경험에서는 "migrationStatus"와 같은 사용자 상태를 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-112">A custom user journey needs to persist the state of user such as "migrationStatus."</span></span>

<span data-ttu-id="a57e5-113">Azure AD B2C를 사용하면 각 사용자 계정에 저장된 특성 집합을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-113">With Azure AD B2C, you can extend the set of attributes stored on each user account.</span></span> <span data-ttu-id="a57e5-114">또한 [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)를 사용하여 이러한 특성을 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-114">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="a57e5-115">확장 속성은 디렉터리에서 사용자 개체의 스키마를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-115">Extension properties extend the schema of the user objects in the directory.</span></span>  <span data-ttu-id="a57e5-116">조건 확장 속성, 사용자 지정 특성 및 사용자 지정 클레임은 이 문서의 컨텍스트에서 동일한 항목을 참조하고 이름은 컨텍스트(응용 프로그램, 개체, 정책)에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-116">The terms extension property, custom attribute and custom claim refer to the same thing in the context of this article and the name varies depending on the context (application, object, policy).</span></span>

<span data-ttu-id="a57e5-117">확장 속성은 사용자에 대한 데이터를 포함할 수 있더라도 응용 프로그램 개체에만 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="a57e5-118">이 속성은 응용 프로그램에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-118">The property is attached to the application.</span></span> <span data-ttu-id="a57e5-119">확장 속성을 등록하려면 응용 프로그램 개체에 쓰기 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-119">The Application object must be granted write access to register an extension property.</span></span> <span data-ttu-id="a57e5-120">단일 개체에 100개의 확장 속성(모든 형식 및 모든 응용 프로그램)을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-120">100 Extension properties (across ALL types and ALL applications) can be written to any single object.</span></span> <span data-ttu-id="a57e5-121">확장 속성이 대상 디렉터리 유형에 추가되고 Azure AD B2C 디렉터리 테넌트에서 즉시 액세스할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-121">Extension properties are added to the target directory type and becomes immediately accessible in the Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="a57e5-122">응용 프로그램이 삭제되면 모든 사용자에 대해 포함된 모든 데이터와 함께 해당 확장 속성도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-122">If the application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="a57e5-123">확장 속성이 응용 프로그램에 의해 삭제되면 대상 디렉터리 개체에서 제거되고 값이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-123">If an extension property is deleted by the Application, it is removed on the target directory objects, and the values deleted.</span></span>

<span data-ttu-id="a57e5-124">확장 속성은 테넌트의 등록된 응용 프로그램 컨텍스트에서만 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-124">Extension properties exist only in the context of a registered  Application in the tenant.</span></span> <span data-ttu-id="a57e5-125">응용 프로그램의 개체 ID는 ID를 사용하는 TechnicalProfile에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-125">The object id of that Application must be included in the TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="a57e5-126">Azure AD B2C 디렉터리는 일반적으로 `b2c-extensions-app`으로 명명된 Web App을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-126">The Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="a57e5-127">이 응용 프로그램은 주로 Azure Portal을 통해 만든 사용자 지정 클레임에 대한 b2c 기본 제공 정책에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-127">This application is primarily used by the b2c built-in  policies for the custom claims created via the Azure portal.</span></span>  <span data-ttu-id="a57e5-128">이 응용 프로그램을 사용하여 b2c 사용자 지정 정책의 확장을 등록하는 것은 고급 사용자에게만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-128">Using this application to register extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="a57e5-129">이에 대한 지침은 이 문서의 다음 단계 섹션에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-129">Instructions for this are included in the Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-to-store-the-extension-properties"></a><span data-ttu-id="a57e5-130">확장 속성을 저장할 새 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a57e5-130">Creating a new application to store the extension properties</span></span>

1. <span data-ttu-id="a57e5-131">브라우저 세션을 열고 [Azure Portal](https://portal.azure.com)로 이동하여 구성할 B2C 디렉터리의 관리 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-131">Open a browsing session and navigate to the [Azure porta](https://portal.azure.com) and sign in with administrative credentials of the B2C Directory you wish to configure.</span></span>
1. <span data-ttu-id="a57e5-132">왼쪽 탐색 메뉴에서 **Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-132">Click **Azure Active Directory** on the left navigation menu.</span></span> <span data-ttu-id="a57e5-133">추가 서비스>를 선택하여 서비스를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-133">You may need to find it by selecting More services>.</span></span>
1. <span data-ttu-id="a57e5-134">**앱 등록**을 선택하고 **새 응용 프로그램 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="a57e5-135">다음 권장되는 항목을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-135">Provide the following recommended entries:</span></span>
  * <span data-ttu-id="a57e5-136">웹 응용 프로그램의 이름 지정: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="a57e5-136">Specify a name for the web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="a57e5-137">응용 프로그램 유형: 웹앱/API</span><span class="sxs-lookup"><span data-stu-id="a57e5-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="a57e5-138">로그온 URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="a57e5-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="a57e5-139">**만들기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-139">Select **Create.</span></span> <span data-ttu-id="a57e5-140">성공적인 완료가 **알림**에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-140">Successful completion appears in the **notifications**</span></span>
1. <span data-ttu-id="a57e5-141">새로 만든 **WebApp-GraphAPI-DirectoryExtensions** 웹 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-141">Select the newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="a57e5-142">**필요한 권한** 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="a57e5-143">**Windows Active Directory** API를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="a57e5-144">**디렉터리 데이터 읽기 및 쓰기** 응용 프로그램 권한을 확인 표시하고 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="a57e5-145">**사용 권한 부여**를 선택하고 **예**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="a57e5-146">클립보드에 복사하고 WebApp-GraphAPI-DirectoryExtensions>Settings>Properties>에서 다음 ID를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-146">Copy to your clipboard and save the following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="a57e5-147">**응용 프로그램 ID** -</span><span class="sxs-lookup"><span data-stu-id="a57e5-147">**Application ID** .</span></span> <span data-ttu-id="a57e5-148">예: `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="a57e5-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="a57e5-149">**개체 ID** -</span><span class="sxs-lookup"><span data-stu-id="a57e5-149">**Object ID**.</span></span> <span data-ttu-id="a57e5-150">예: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="a57e5-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-to-add-the-applicationobjectid"></a><span data-ttu-id="a57e5-151">사용자 지정 정책을 수정하여 ApplicationObjectId 추가</span><span class="sxs-lookup"><span data-stu-id="a57e5-151">Modifying your custom policy to add the ApplicationObjectId</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
><span data-ttu-id="a57e5-152">해당 요소가 해당 요소를 사용하여 모든 Azure Active Directory TechnicalProfiles에 포함되고 재사용되기 때문에 <TechnicalProfile Id="AAD-Common">은 "공용"입니다.`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="a57e5-152">The <TechnicalProfile Id="AAD-Common"> is referred to as "common" because its elements are included in and reused in all the Azure Active Directory TechnicalProfiles by using the element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="a57e5-153">TechnicalProfile이 처음 새로 작성된 확장 속성에 작성되는 경우 일회성 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-153">When the TechnicalProfile writes for the first time to the newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="a57e5-154">확장 속성은 처음 사용할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-154">The extension property is created the first time it is used.</span></span>  

## <a name="using-the-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="a57e5-155">사용자 경험에서 새 확장 속성/사용자 지정 특성 사용</span><span class="sxs-lookup"><span data-stu-id="a57e5-155">Using the new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="a57e5-156">정책 편집 사용자 경험을 설명하는 신뢰 당사자(RP) 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-156">Open the Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="a57e5-157">시작하는 경우 Azure Portal의 Azure B2C 사용자 지정 정책 섹션에서 RP-PolicyEdit 파일의 이미 구성된 버전을 직접 다운로드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-157">If you are starting out, it may be advisable to download your already configured version of the RP-PolicyEdit file directly from the Azure B2C Custom Policy section in the Azure portal.</span></span>  <span data-ttu-id="a57e5-158">또는 저장소 폴더에서 XML 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="a57e5-159">사용자 지정 클레임 `loyaltyId`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="a57e5-160">`<RelyingParty>` 요소에 사용자 지정 클레임을 포함하면 UserJourney TechnicalProfiles에 매개 변수로 전달되고 응용 프로그램의 토큰에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-160">By including the custom claim in the `<RelyingParty>` element, it is passed as a parameter to the UserJourney TechnicalProfiles and included in the token for the application.</span></span>
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. <span data-ttu-id="a57e5-161">표시된 것처럼 `<ClaimsSchema>` 요소 내부 확장 정책 파일 `TrustFrameworkExtensions.xml`에 클레임 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-161">Add a claim definition to the Extension policy file  `TrustFrameworkExtensions.xml` inside the `<ClaimsSchema>` element as shown.</span></span>
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. <span data-ttu-id="a57e5-162">동일한 클레임 정의를 기본 정책 파일 `TrustFrameworkBase.xml`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-162">Add the same claim definition to the Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="a57e5-163">기본 및 확장 파일 모두에 `ClaimType` 정의를 추가하는 것은 일반적으로 필요하지 않지만, 다음 단계에서 기본 파일의 TechnicalProfiles에 extension_loyaltyId를 추가하므로 정책 유효성 검사기에서 해당 정의가 없는 기본 파일의 업로드를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-163">Adding a `ClaimType` definition in both the base and the extensions file is normally not necessary, however since the next steps will add the extension_loyaltyId to TechnicalProfiles in the Base file, the policy validator will reject the upload of the base file without it.</span></span>
><span data-ttu-id="a57e5-164">TrustFrameworkBase.xml 파일에서 "ProfileEdit"라는 사용자 경험의 실행을 추적하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-164">It may be useful to trace the execution of the user journey named "ProfileEdit" in the TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="a57e5-165">편집기에서 같은 이름의 사용자 경험을 검색하고 오케스트레이션 5단계에서 TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate"를 호출하는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-165">Search for the user journey of the same name in your editor and observe that Orchestration Step 5 invokes the TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="a57e5-166">이 TechnicalProfile을 검색 및 검사하여 흐름에 익숙해 지도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-166">Search and inspect this TechnicalProfile to familiarize yourself with the flow.</span></span>
5. <span data-ttu-id="a57e5-167">TechnicalProfile "SelfAsserted-ProfileUpdate"에서 입력 및 출력 클레임으로 loyaltyId를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-167">Add loyaltyId as input and output claim in the TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="a57e5-168">TechnicalProfile "AAD-UserWriteProfileUsingObjectId"에서 클레임을 추가하여 클레임 값을 디렉터리의 현재 사용자에 대한 확장 속성에서 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" to persist the value of the claim in the extension property, for the current user in the directory.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. <span data-ttu-id="a57e5-169">TechnicalProfile "AAD-UserReadUsingObjectId"에서 클레임을 추가하여 사용자가 로그인할 때마다 확장 특성 값을 읽어 옵니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" to read the value of the extension attribute every time a user logs in.</span></span> <span data-ttu-id="a57e5-170">지금까지 로컬 계정의 흐름에서만 TechnicalProfiles가 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-170">Thus far the TechnicalProfiles have been changed in the flow of local accounts only.</span></span>  <span data-ttu-id="a57e5-171">소셜/페더레이션된 계정의 흐름에 새 특성이 필요한 경우 다른 TechnicalProfiles 집합을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-171">If the new attribute is desired in the flow of a social/federated account, a different set of TechnicalProfiles needs to be changed.</span></span> <span data-ttu-id="a57e5-172">다음 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a57e5-172">See Next Steps.</span></span>

```xml
<!-- The following technical profile is used to read data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
><span data-ttu-id="a57e5-173">IncludeTechnicalProfile 요소는 AAD-Common의 모든 요소를 이 TechnicalProfile에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-173">The IncludeTechnicalProfile element adds all the elements of AAD-Common to this TechnicalProfile.</span></span>

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="a57e5-174">"지금 실행"을 사용하여 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="a57e5-174">Test the custom policy using "Run Now"</span></span>
1. <span data-ttu-id="a57e5-175">**Azure AD B2C 블레이드**를 열고 **ID 경험 프레임워크 > 사용자 지정 정책**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-175">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="a57e5-176">업로드한 사용자 지정 정책을 선택하고 **지금 실행** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-176">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
1. <span data-ttu-id="a57e5-177">전자 메일 주소를 사용하여 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-177">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="a57e5-178">응용 프로그램으로 다시 전송된 ID 토큰에는 extension_loyaltyId가 앞에 오는 사용자 지정 클레임으로 새로운 확장 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-178">The  id token sent back to your application includes the new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="a57e5-179">예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a57e5-179">See example.</span></span>

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="a57e5-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a57e5-180">Next steps</span></span>

<span data-ttu-id="a57e5-181">나열된 TechnicalProfiles를 변경하여 새 클레임을 소셜 계정 로그인에 대한 흐름에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-181">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed.</span></span> <span data-ttu-id="a57e5-182">이러한 두 TechnicalProfiles는 사용자 개체의 로케이터로 alternativeSecurityId를 사용하여 사용자 데이터를 쓰고 읽기 위해 소셜/페더레이션된 계정 로그인에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-182">These two TechnicalProfiles are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator of the user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="a57e5-183">기본 및 사용자 지정 정책 간에 동일한 확장 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-183">Using the same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="a57e5-184">포털 환경을 통해 확장 특성(즉, 사용자 지정 특성)을 추가하는 경우 해당 특성은 모든 b2c 테넌트에 존재하는 **b2c-extensions-app을 사용하여 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-184">When you add extension attributes (aka custom attributes) via the portal experience, those attributes are registered using the **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="a57e5-185">사용자 지정 정책에서 이러한 확장 특성을 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="a57e5-185">To use these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="a57e5-186">portal.azure.com의 b2c 테넌트 내에서 **Azure Active Directory**로 이동하고 **앱 등록** 선택</span><span class="sxs-lookup"><span data-stu-id="a57e5-186">Within your b2c tenant in portal.azure.com, navigate to **Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="a57e5-187">**b2c-확장-앱**을 찾고 선택</span><span class="sxs-lookup"><span data-stu-id="a57e5-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="a57e5-188">'Essentials' 아래에서 **응용 프로그램 ID** 및 **개체 ID** 기록</span><span class="sxs-lookup"><span data-stu-id="a57e5-188">Under 'Essentials' record the **Application ID** and the **Object ID**</span></span>
4. <span data-ttu-id="a57e5-189">다음과 같이 AAD 공용 기술 프로필 메타데이터에 포함:</span><span class="sxs-lookup"><span data-stu-id="a57e5-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is the "Object ID" from the "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is the "Application ID" from the "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="a57e5-190">포털 환경과 일관성을 유지하기 위해 사용자 지정 정책에서 사용하기 *전에* 포털 UI를 사용하여 이러한 특성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-190">To keep consistency with the portal experience, create these attributes using the portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="a57e5-191">포털에서 "ActivationStatus" 특성을 만들 때 다음과 같이 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-191">When you create an attribute "ActivationStatus" in the portal, you must refer to it as follows:</span></span>

```
extension_ActivationStatus in the custom policy
extension_<app-guid>_ActivationStatus via the Graph API.
```


## <a name="reference"></a><span data-ttu-id="a57e5-192">참조</span><span class="sxs-lookup"><span data-stu-id="a57e5-192">Reference</span></span>

* <span data-ttu-id="a57e5-193">**TP(기술 프로필)**은 끝점의 이름, 해당 메타데이터, 해당 프로토콜을 정의하고 Identity Experience Framework가 수행해야 하는 클레임의 교환에 대해 자세히 설명하는 *함수*로 간주할 수 있는 요소 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details the exchange of claims that the Identity Experience Framework should perform.</span></span>  <span data-ttu-id="a57e5-194">오케스트레이션 단계 또는 다른 TechnicalProfile에서 이 *함수*를 호출하면 InputClaims 및 OutputClaims가 호출자의 매개 변수로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-194">When this *function* is called in an orchestration step or from another TechnicalProfile, the InputClaims and OutputClaims are provided as parameters by the caller.</span></span>


* <span data-ttu-id="a57e5-195">확장 속성에 대한 완전한 처리는 [디렉터리 스키마 확장 | Graph API 개념](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a57e5-195">For full treatment on extension properties, see the article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="a57e5-196">Graph API의 확장 특성은 `extension_ApplicationObjectID_attributename` 규칙을 사용하여 명명됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-196">Extension attributes in Graph API are named using the convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="a57e5-197">사용자 지정 정책은 확장 특성을 extension_attributename으로 참조하므로 XML에서 ApplicationObjectId가 생략됩니다.</span><span class="sxs-lookup"><span data-stu-id="a57e5-197">Custom policies refer to extensions attributes as extension_attributename, thus omitting the ApplicationObjectId in the XML</span></span>
