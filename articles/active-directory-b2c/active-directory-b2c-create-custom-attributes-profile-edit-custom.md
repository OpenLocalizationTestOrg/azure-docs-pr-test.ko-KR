---
title: "Azure Active Directory B2C: 사용자의 고유한 특성 toocustom 정책을 추가 하 고 프로필 편집에 사용 하 | Microsoft Docs"
description: "확장 속성을 사용자 지정 특성을 사용 하 고 hello 사용자 인터페이스에 포함 하는 연습"
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
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="17d40-103">Azure Active Directory B2C: 사용자 지정 프로필 편집 정책에서 사용자 지정 특성을 만들고 사용</span><span class="sxs-lookup"><span data-stu-id="17d40-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="17d40-104">이 문서에서는 Azure AD B2C 디렉터리에 사용자 지정 특성을 만들 및 hello 프로필 편집 사용자 작업의 사용자 지정 클레임으로이 새 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17d40-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="17d40-105">Prerequisites</span></span>

<span data-ttu-id="17d40-106">Hello 문서에서 단계를 완료 하는 hello [사용자 지정 정책을 사용 하 여 시작](active-directory-b2c-get-started-custom.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="17d40-107">사용자 지정 정책을 사용 하 여 Azure Active Directory B2C에 고객에 대 한 사용자 지정 특성 toocollect 정보를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="17d40-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="17d40-108">Azure Active Directory(Azure AD) B2C 디렉터리에는 지정된 이름, 성, 도시, 우편 번호, userPrincipalName의 특성 집합이 함께 제공됩니다.  Toocreate 사용자 고유의 특성 주로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="17d40-109">예:</span><span class="sxs-lookup"><span data-stu-id="17d40-109">For example:</span></span>
* <span data-ttu-id="17d40-110">고객 지향 응용 프로그램이 있어야 toopersist "LoyaltyNumber."와 같은 특성</span><span class="sxs-lookup"><span data-stu-id="17d40-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="17d40-111">ID 공급자는 "uniqueUserGUID"처럼 저장해야 하는 고유한 사용자 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="17d40-112">사용자 지정 사용자 여행 필요 "migrationStatus."와 같은 사용자의 toopersist hello 상태</span><span class="sxs-lookup"><span data-stu-id="17d40-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="17d40-113">Azure AD B2C hello 각 사용자 계정에 저장 하는 특성 집합을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="17d40-114">또한 읽고 수 hello를 사용 하 여 이러한 특성을 쓸 [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="17d40-115">확장 속성 hello 디렉터리에 hello 사용자 개체의 hello 스키마를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="17d40-116">hello 용어 확장 속성, 사용자 지정 특성 및 사용자 지정 클레임 toohello hello 컨텍스트 (응용 프로그램, 개체, 정책)에 따라 달라 집니다이 문서와 hello 이름의 hello 컨텍스트에서 동일한 작업을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="17d40-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="17d40-117">확장 속성은 사용자에 대한 데이터를 포함할 수 있더라도 응용 프로그램 개체에만 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="17d40-118">hello 속성은 연결 된 toohello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-118">hello property is attached toohello application.</span></span> <span data-ttu-id="17d40-119">hello 응용 프로그램 개체에는 쓰기 권한을 부여한 tooregister 확장 속성 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="17d40-120">(모든 형식 및 모든 응용 프로그램)에서 확장 속성을 100 tooany 단일 개체를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="17d40-121">확장 속성 toohello 대상 디렉터리 유형에 추가 되 고 hello Azure AD B2C 디렉터리 테 넌 트에 즉시 액세스할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="17d40-122">Hello 응용 프로그램을 삭제 하면 모든 사용자에 대해 여기에 포함 된 데이터와 함께 해당 확장 속성 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="17d40-123">Hello에 없어지기 hello 응용 프로그램에서 확장 속성 삭제 되 면 대상 디렉터리 개체 및 hello 삭제 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="17d40-124">확장 속성 hello 테 넌 트에 등록된 된 응용 프로그램의 hello 컨텍스트 에서만에서 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="17d40-125">해당 응용 프로그램의 개체 id hello TechnicalProfile 사용 하는 hello에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="17d40-126">hello Azure AD B2C 디렉터리 라는 웹 앱을 일반적으로 포함 `b2c-extensions-app`합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="17d40-127">이 응용 프로그램은 주로 hello Azure 포털을 통해 만든 hello 사용자 지정 클레임에 대 한 hello b2c에 대 한 기본 제공 정책에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="17d40-128">고급 사용자에 게이 응용 프로그램 tooregister 확장을 사용 하 여 b2c 사용자 지정 정책에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="17d40-129">이 대 한 지침은이 문서의 다음 단계 섹션 hello에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="17d40-130">새 응용 프로그램 toostore hello 확장 속성 만들기</span><span class="sxs-lookup"><span data-stu-id="17d40-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="17d40-131">검색 세션을 열고 toohello 이동 [Azure 포털](https://portal.azure.com) hello tooconfigure B2C 디렉터리의 관리자 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="17d40-132">클릭 **Azure Active Directory** hello 왼쪽된 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="17d40-133">선택 하 여 더 명의 toofind 할 수 있습니다 > 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="17d40-134">**앱 등록**을 선택하고 **새 응용 프로그램 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="17d40-135">Hello 다음 권장 항목을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="17d40-136">Hello 웹 응용 프로그램에 대 한 이름을 지정: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="17d40-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="17d40-137">응용 프로그램 유형: 웹앱/API</span><span class="sxs-lookup"><span data-stu-id="17d40-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="17d40-138">로그온 URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="17d40-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="17d40-139">**만들기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-139">Select **Create.</span></span> <span data-ttu-id="17d40-140">Hello에 성공적으로 완료 표시 **알림**</span><span class="sxs-lookup"><span data-stu-id="17d40-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="17d40-141">새로 만든 hello 웹 응용 프로그램 선택: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="17d40-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="17d40-142">**필요한 권한** 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="17d40-143">**Windows Active Directory** API를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="17d40-144">**디렉터리 데이터 읽기 및 쓰기** 응용 프로그램 권한을 확인 표시하고 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="17d40-145">**사용 권한 부여**를 선택하고 **예**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="17d40-146">Tooyour 클립보드를 복사 하 고 hello 식별자 WebApp-GraphAPI-DirectoryExtensions에서 다음 저장 > 설정 > 속성 ></span><span class="sxs-lookup"><span data-stu-id="17d40-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="17d40-147">**응용 프로그램 ID** -</span><span class="sxs-lookup"><span data-stu-id="17d40-147">**Application ID** .</span></span> <span data-ttu-id="17d40-148">예: `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="17d40-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="17d40-149">**개체 ID** -</span><span class="sxs-lookup"><span data-stu-id="17d40-149">**Object ID**.</span></span> <span data-ttu-id="17d40-150">예: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="17d40-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="17d40-151">사용자 지정 정책 tooadd hello ApplicationObjectId 수정</span><span class="sxs-lookup"><span data-stu-id="17d40-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

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
><span data-ttu-id="17d40-152">hello <TechnicalProfile Id="AAD-Common"> 해당 요소에 포함 되어 hello 요소를 사용 하 여 모든 hello Azure Active Directory TechnicalProfiles에서에서 다시 사용 하기 때문에 참조 된 tooas "공용" 됩니다.`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="17d40-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="17d40-153">Hello TechnicalProfile hello 첫 번째 시간 toohello 새로 만든 확장 속성을 기록 하는 경우 일회성 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="17d40-154">hello 확장 속성은 만들어집니다 hello 처음으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="17d40-155">Hello 새 확장 속성을 사용 하 여 사용자 지정 특성을 사용자 여행 /</span><span class="sxs-lookup"><span data-stu-id="17d40-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="17d40-156">정책에 설명 하는 신뢰 Party(RP) 파일 열기 hello 사용자 작업을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="17d40-157">시작 하는 경우 프로그램 이미 구성 된 버전의 hello RP PolicyEdit hello hello Azure 포털에서에서 Azure B2C 사용자 지정 정책 섹션에서 직접 파일 권장 toodownload 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="17d40-158">또는 저장소 폴더에서 XML 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="17d40-159">사용자 지정 클레임 `loyaltyId`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="17d40-160">Hello 사용자 지정을 포함 하 여 hello에 클레임 `<RelyingParty>` 요소, 매개 변수 toohello UserJourney TechnicalProfiles 변수로 전달 되 고 hello 응용 프로그램에 대 한 hello 토큰에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
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
3. <span data-ttu-id="17d40-161">클레임 정의 toohello 확장명 정책 파일을 추가 `TrustFrameworkExtensions.xml` hello 내 `<ClaimsSchema>` 요소와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
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
4. <span data-ttu-id="17d40-162">Hello 추가 정의 toohello 기본 정책 파일을 클레임 동일 `TrustFrameworkBase.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="17d40-163">하지만 추가 `ClaimType` hello 자료 및 hello 확장 파일 정의 일반적으로 필요 hello 정책 유효성 검사기는 hello 업로드를 거부 hello 다음 단계 hello extension_loyaltyId tooTechnicalProfiles hello 기본 파일에서을 추가 하는 이후 hello 없이 기본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="17d40-164">Hello TrustFrameworkBase.xml 파일에서 "ProfileEdit" 라는 hello 사용자 작업의 유용한 tootrace hello 실행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="17d40-165">Hello 동일 하면 편집기의 이름을 지정 하 고 5 단계 오케스트레이션 호출 hello TechnicalProfileReferenceID 있는지 관찰의 hello 사용자 작업에 대 한 검색 "SelfAsserted ProfileUpdate" = 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="17d40-166">검색 하 고 hello 흐름에 따라 직접이 TechnicalProfile toofamiliarize를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="17d40-167">Hello TechnicalProfile "SelfAsserted ProfileUpdate"의 입력 및 출력 클레임으로 loyaltyId 추가</span><span class="sxs-lookup"><span data-stu-id="17d40-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
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

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="17d40-168">Hello hello 디렉터리의 현재 사용자에 대 한 hello 확장 속성에 hello 클레임의 TechnicalProfile "AAD UserWriteProfileUsingObjectId" toopersist hello 값에 클레임을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
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
7. <span data-ttu-id="17d40-169">사용자가 로그인 할 때마다 TechnicalProfile "AAD UserReadUsingObjectId" tooread hello hello 확장 특성 값에 클레임을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="17d40-170">지금까지 hello TechnicalProfiles 로컬 계정의 hello 흐름에서 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="17d40-171">사회/페더레이션 계정의 hello 흐름에서 hello 새 특성을 사용할 경우 다른 집합이 TechnicalProfiles toobe 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="17d40-172">다음 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17d40-172">See Next Steps.</span></span>

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
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
><span data-ttu-id="17d40-173">hello IncludeTechnicalProfile 요소 AAD 공통 toothis TechnicalProfile의 모든 hello 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="17d40-174">"Run Now"를 사용 하 여 hello 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="17d40-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="17d40-175">열기 hello **Azure AD B2C 블레이드** 너무 이동**Id 경험 프레임 워크 > 사용자 지정 정책의**합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="17d40-176">업로드 하는 hello 사용자 지정 정책을 선택 하 고 hello 클릭 **지금 실행** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="17d40-177">전자 메일 주소를 사용 하 여 수 toosign 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="17d40-178">hello id 토큰 tooyour 응용 프로그램을 사용자 지정 클레임 extension_loyaltyId 앞으로 hello 새 확장 속성에 다시 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="17d40-179">예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17d40-179">See example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="17d40-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17d40-180">Next steps</span></span>

<span data-ttu-id="17d40-181">TechnicalProfiles 나열 된 hello를 변경 하 여 소셜 계정 로그인에 대 한 hello 새 클레임 toohello 흐름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="17d40-182">이러한 두 TechnicalProfiles 사회/페더레이션 계정 로그인 toowrite 사용 하 고 hello 사용자 개체의 로케이터 hello hello alternativeSecurityId 사용 하 여 hello 사용자 데이터를 읽이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="17d40-183">기본 및 사용자 지정 정책 간에 동일한 확장 특성 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="17d40-184">Hello를 사용 하 여 이러한 특성은 등록 hello 포털 경험을 통해 확장 특성 (즉, 사용자 지정 특성의 경우)를 추가 하면 * * b2c-확장-app 모든 b2c 테 넌 트에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="17d40-185">toouse 사용자 지정 정책에서 이러한 확장 특성:</span><span class="sxs-lookup"><span data-stu-id="17d40-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="17d40-186">B2c 테 넌 트에 portal.azure.com 내에서 이동 너무**Azure Active Directory** 선택 **앱 등록**</span><span class="sxs-lookup"><span data-stu-id="17d40-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="17d40-187">**b2c-확장-앱**을 찾고 선택</span><span class="sxs-lookup"><span data-stu-id="17d40-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="17d40-188">'Essentials' 레코드 hello에서 **응용 프로그램 ID** 및 hello **개체 ID**</span><span class="sxs-lookup"><span data-stu-id="17d40-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="17d40-189">다음과 같이 AAD 공용 기술 프로필 메타데이터에 포함:</span><span class="sxs-lookup"><span data-stu-id="17d40-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="17d40-190">hello 포털 환경과 tookeep 일관성 hello 포털 UI를 사용 하 여 이러한 특성을 만들 *전에* 지정 정책에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="17d40-191">를 만들 때 특성 "ActivationStatus" hello 포털에서 다음과 같이 tooit을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="17d40-192">참조</span><span class="sxs-lookup"><span data-stu-id="17d40-192">Reference</span></span>

* <span data-ttu-id="17d40-193">A **기술 프로필 (TP)** 요소 형식인로 간주 될 수 있는 한 *함수* 끝점의 이름, 해당 메타 데이터, 해당 프로토콜을 정의 하 고 세부 정보 hello Identity hello 클레임 교환을 경험 프레임 워크를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="17d40-194">때이 *함수* 다른 TechnicalProfile, InputClaims 및 OutputClaims은 hello 호출자가 매개 변수로 제공 됩니다 hello 또는 오케스트레이션 단계에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="17d40-195">확장 속성에 대해 전체 처리를 위해 hello 문서 참조 [디렉터리 스키마 확장 | GRAPH API 개념](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="17d40-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="17d40-196">Hello 규칙을 사용 하 여 Graph API에 대 한 확장 특성 이름은 `extension_ApplicationObjectID_attributename`합니다.</span><span class="sxs-lookup"><span data-stu-id="17d40-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="17d40-197">따라서 XML hello에 ApplicationObjectId hello 생략 extension_attributename로 tooextensions 특성을 참조 하는 사용자 지정 정책</span><span class="sxs-lookup"><span data-stu-id="17d40-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
