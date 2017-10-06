---
title: "사용자 지정 정책을 사용하여 UI 사용자 지정 - Azure AD B2C | Microsoft Docs"
description: "Azure AD B2C에서 사용자 지정 정책을 사용하는 동안 UI(사용자 인터페이스)를 사용자 지정하는 방법에 대해 알아봅니다."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="bdaaf-103">Azure Active Directory B2C: 사용자 지정 정책에서 UI 사용자 지정 구성</span><span class="sxs-lookup"><span data-stu-id="bdaaf-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="bdaaf-104">이 문서를 완료하면 브랜드와 모양이 포함된 등록 및 로그인 사용자 지정 정책을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="bdaaf-105">와 Azure Active Directory B2C (Azure AD B2C) hello HTML 및 CSS 콘텐츠의 거의 모든 권한 있는 게 toousers 제시한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of hello HTML and CSS content that's presented toousers.</span></span> <span data-ttu-id="bdaaf-106">사용자 지정 정책을 사용 하는 경우 구성한 UI 사용자 지정 xml에서 hello Azure 포털에서에서 컨트롤을 사용 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-106">When you use a custom policy, you configure UI customization in XML instead of using controls in hello Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bdaaf-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bdaaf-107">Prerequisites</span></span>

<span data-ttu-id="bdaaf-108">시작하기 전에 먼저 [사용자 지정 정책 시작](active-directory-b2c-get-started-custom.md)을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="bdaaf-109">로컬 계정을 사용하여 등록 및 로그인하기 위한 사용자 지정 정책이 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="bdaaf-110">페이지 UI 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="bdaaf-110">Page UI customization</span></span>

<span data-ttu-id="bdaaf-111">Hello 페이지 UI 사용자 지정 기능을 사용 하 여 hello의 디자인을 사용자 지정 정책 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-111">By using hello page UI customization feature, you can customize hello look and feel of any custom policy.</span></span> <span data-ttu-id="bdaaf-112">또한 응용 프로그램과 Azure AD B2C 간에 브랜드와 시각적 개체 일관성을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="bdaaf-113">작동 방식은 다음과 같습니다. Azure AD B2C는 소비자의 브라우저에서 코드를 실행하고 [CORS(원본 간 리소스 공유)](http://www.w3.org/TR/cors/)라는 최신의 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="bdaaf-114">첫째, 사용자 지정 된 HTML 콘텐츠가 있는 사용자 지정 정책 hello에에서 URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-114">First, you specify a URL in hello custom policy with customized HTML content.</span></span> <span data-ttu-id="bdaaf-115">Azure AD B2C hello URL에서 로드 되 고 다음 hello 페이지 toohello 고객을 표시 하는 HTML 콘텐츠를 사용 하 여 UI 요소를 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-115">Azure AD B2C merges UI elements with hello HTML content that's loaded from your URL and then displays hello page toohello customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="bdaaf-116">HTML5 콘텐츠 만들기</span><span class="sxs-lookup"><span data-stu-id="bdaaf-116">Create your HTML5 content</span></span>

<span data-ttu-id="bdaaf-117">Hello 제목에 HTML 콘텐츠를 제품의 브랜드 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-117">Create HTML content with your product's brand name in hello title.</span></span>

1. <span data-ttu-id="bdaaf-118">다음 HTML 코드 조각을 hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-118">Copy hello following HTML snippet.</span></span> <span data-ttu-id="bdaaf-119">올바른 형식이 HTML5 빈 요소와 함께 호출 * \<div id = "api"\>\</div\> * hello 내에 있는 * \<본문\> * 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within hello *\<body\>* tags.</span></span> <span data-ttu-id="bdaaf-120">이 요소는 Azure AD B2C 콘텐츠인지 toobe 삽입 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-120">This element indicates where Azure AD B2C content is toobe inserted.</span></span>

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   ><span data-ttu-id="bdaaf-121">보안상의 이유로 hello를 사용 하 여 JavaScript의 현재 차단 된 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-121">For security reasons, hello use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="bdaaf-122">텍스트 편집기에 복사 hello 조각을 다음으로 hello 파일을 저장 *사용자 지정 ui.html*합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-122">Paste hello copied snippet in a text editor, and then save hello file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="bdaaf-123">Azure Blob 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="bdaaf-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="bdaaf-124">이 문서에서 사용 하 여 Azure Blob 저장소 toohost 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-124">In this article, we use Azure Blob storage toohost our content.</span></span> <span data-ttu-id="bdaaf-125">웹 서버에서 콘텐츠 toohost를 선택할 수 있지만 해야 [CORS 웹 서버에서 사용할](https://enable-cors.org/server.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-125">You can choose toohost your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="bdaaf-126">toohost Blob 저장소에이 HTML 콘텐츠에 따라 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-126">toohost this HTML content in Blob storage, do hello following:</span></span>

1. <span data-ttu-id="bdaaf-127">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-127">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bdaaf-128">Hello에 **허브** 메뉴 선택 **새로** > **저장소** > **저장소 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-128">On hello **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="bdaaf-129">저장소 계정의 고유한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="bdaaf-130">**배포 모델**은 **Resource Manager**로 유지하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="bdaaf-131">변경 **계정 종류** 너무**Blob 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-131">Change **Account Kind** too**Blob storage**.</span></span>
6. <span data-ttu-id="bdaaf-132">**성능**은 **표준**으로 유지하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="bdaaf-133">**복제**는**RA-GRS**로 유지하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="bdaaf-134">**액세스 계층**은 **핫**으로 유지하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="bdaaf-135">**저장소 서비스 암호화**는 **사용 안 함**으로 유지하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="bdaaf-136">저장소 계정에 대한 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="bdaaf-137">**리소스 그룹**을 만들거나 기존 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="bdaaf-138">선택 hello **지리적 위치** 저장소 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-138">Select hello **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="bdaaf-139">클릭 **만들기** toocreate hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-139">Click **Create** toocreate hello storage account.</span></span>  
    <span data-ttu-id="bdaaf-140">Hello 배포가 완료 된 후 hello **저장소 계정** 블레이드 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-140">After hello deployment is completed, hello **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="bdaaf-141">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="bdaaf-141">Create a container</span></span>

<span data-ttu-id="bdaaf-142">Blob 저장소에서 공개 컨테이너 toocreate 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-142">toocreate a public container in Blob storage, do hello following:</span></span>

1. <span data-ttu-id="bdaaf-143">Hello 클릭 **개요** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-143">Click hello **Overview** tab.</span></span>
2. <span data-ttu-id="bdaaf-144">**컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-144">Click **Container**.</span></span>
3. <span data-ttu-id="bdaaf-145">**이름**으로 **$root**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="bdaaf-146">설정 **액세스 형식** 너무**Blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-146">Set **Access type** too**Blob**.</span></span>
5. <span data-ttu-id="bdaaf-147">클릭 **$root** tooopen hello 새 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-147">Click **$root** tooopen hello new container.</span></span>
6. <span data-ttu-id="bdaaf-148">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-148">Click **Upload**.</span></span>
7. <span data-ttu-id="bdaaf-149">다음 너무 hello 폴더 아이콘을 클릭**파일 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-149">Click hello folder icon next too**Select a file**.</span></span>
8. <span data-ttu-id="bdaaf-150">너무 이동**사용자 지정 ui.html**, hello 앞부분에서 만든 [페이지 UI 사용자 지정](#the-page-ui-customization-feature) 섹션.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-150">Go too**customize-ui.html**, which you created earlier in hello [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="bdaaf-151">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-151">Click **Upload**.</span></span>
10. <span data-ttu-id="bdaaf-152">업로드 hello ui.html 사용자 지정 blob을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-152">Select hello customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="bdaaf-153">다음 너무**URL**, 클릭 **복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-153">Next too**URL**, click **Copy**.</span></span>
12. <span data-ttu-id="bdaaf-154">브라우저에서 hello 복사한 URL을 붙여 넣고 toohello 사이트 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-154">In a browser, paste hello copied URL, and go toohello site.</span></span> <span data-ttu-id="bdaaf-155">Hello 사이트에 액세스할 수 없는 경우 hello 컨테이너 액세스 형식을 너무 설정 되어 있는지 확인**blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-155">If hello site is inaccessible, make sure hello container access type is set too**blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="bdaaf-156">CORS 구성</span><span class="sxs-lookup"><span data-stu-id="bdaaf-156">Configure CORS</span></span>

<span data-ttu-id="bdaaf-157">Hello 다음을 수행 하 여 크로스-원본 자원 공유에 대 한 Blob 저장소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-157">Configure Blob storage for Cross-Origin Resource Sharing by doing hello following:</span></span>

>[!NOTE]
><span data-ttu-id="bdaaf-158">샘플 HTML 및 CSS 콘텐츠를 사용 하 여 hello UI 사용자 지정 기능을 미리 tootry를 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-158">Want tootry out hello UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="bdaaf-159">Azure Blob 저장소 계정에 샘플 콘텐츠를 업로드하고 구성하는 [간단한 도우미 도구](active-directory-b2c-reference-ui-customization-helper-tool.md)를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="bdaaf-160">Hello 도구를 사용 하면 건너뛰어 너무[등록 또는 로그인 시 사용자 지정 정책을 수정](#modify-your-sign-up-or-sign-in-custom-policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-160">If you use hello tool, skip ahead too[Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="bdaaf-161">Hello에 **저장소** 블레이드 아래 **설정**개방형 **CORS**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-161">On hello **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="bdaaf-162">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-162">Click **Add**.</span></span>
3. <span data-ttu-id="bdaaf-163">**허용된 원본**의 경우 별표(\*)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="bdaaf-164">Hello에 **허용 된 동사** 드롭 다운 목록, 선택 **가져오기** 및 **옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-164">In hello **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="bdaaf-165">**허용된 헤더**의 경우 별표(\*)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="bdaaf-166">**노출된 헤더**의 경우 별표(\*)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="bdaaf-167">**최대 기간(초)**의 경우 **200**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="bdaaf-168">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="bdaaf-169">CORS 테스트</span><span class="sxs-lookup"><span data-stu-id="bdaaf-169">Test CORS</span></span>

<span data-ttu-id="bdaaf-170">준비가 되 hello 다음을 수행 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-170">Validate that you're ready by doing hello following:</span></span>

1. <span data-ttu-id="bdaaf-171">Toohello 이동 [테스트 cors.org](http://test-cors.org/) 웹 사이트로 이동한 다음 hello에 붙여넣기 hello URL **원격 URL** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-171">Go toohello [test-cors.org](http://test-cors.org/) website, and then paste hello URL in hello **Remote URL** box.</span></span>
2. <span data-ttu-id="bdaaf-172">**요청 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="bdaaf-173">오류가 발생하는 경우 [CORS 설정](#configure-cors)이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="bdaaf-174">Tooclear 브라우저 캐시를 필요 또는 Ctrl + Shift + P를 눌러 개인 탐색 세션을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-174">You might also need tooclear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="bdaaf-175">등록 또는 로그인 사용자 지정 정책 수정</span><span class="sxs-lookup"><span data-stu-id="bdaaf-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="bdaaf-176">최상위 hello에서 * \<TrustFrameworkPolicy\> * 태그를 찾아야 * \<직접\> * 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-176">Under hello top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="bdaaf-177">Hello 내 * \<직접\> * 태그, 추가 * \<ContentDefinitions\> * hello 다음 예제를 복사 하 여는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-177">Within hello *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying hello following example.</span></span> <span data-ttu-id="bdaaf-178">대체 *your_storage_account* hello 저장소 계정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-178">Replace *your_storage_account* with hello name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="bdaaf-179">업데이트된 사용자 지정 정책 업로드</span><span class="sxs-lookup"><span data-stu-id="bdaaf-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="bdaaf-180">Hello에 [Azure 포털](https://portal.azure.com), [Azure AD B2C 테 넌 트의 hello 컨텍스트로 전환](active-directory-b2c-navigate-to-b2c-context.md)를 연 다음 hello **Azure AD B2C** 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-180">In hello [Azure portal](https://portal.azure.com), [switch into hello context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open hello **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="bdaaf-181">**모든 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="bdaaf-182">**업로드 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="bdaaf-183">업로드 `SignUpOrSignin.xml` hello로 * \<ContentDefinitions\> * 태그 이전에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-183">Upload `SignUpOrSignin.xml` with hello *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="bdaaf-184">Hello 사용자 지정 정책을 사용 하 여 테스트 **지금 실행**</span><span class="sxs-lookup"><span data-stu-id="bdaaf-184">Test hello custom policy by using **Run now**</span></span>

1. <span data-ttu-id="bdaaf-185">Hello에 **Azure AD B2C** 블레이드에서 너무 이동**정책을 모든**합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-185">On hello **Azure AD B2C** blade, go too**All polices**.</span></span>
2. <span data-ttu-id="bdaaf-186">업로드 하는 hello 사용자 지정 정책을 선택 하 고 hello 클릭 **지금 실행** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-186">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="bdaaf-187">전자 메일 주소를 사용 하 여를 toosign 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-187">You should be able toosign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="bdaaf-188">참조</span><span class="sxs-lookup"><span data-stu-id="bdaaf-188">Reference</span></span>

<span data-ttu-id="bdaaf-189">UI 사용자 지정을 위한 샘플 템플릿은 다음에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="bdaaf-190">hello sample_templates/wingtip 폴더 hello를 다음 HTML 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-190">hello sample_templates/wingtip folder contains hello following HTML files:</span></span>

| <span data-ttu-id="bdaaf-191">HTML5 템플릿</span><span class="sxs-lookup"><span data-stu-id="bdaaf-191">HTML5 template</span></span> | <span data-ttu-id="bdaaf-192">설명</span><span class="sxs-lookup"><span data-stu-id="bdaaf-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="bdaaf-193">*phonefactor.html*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-193">*phonefactor.html*</span></span> | <span data-ttu-id="bdaaf-194">다단계 인증 페이지의 템플릿으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="bdaaf-195">*resetpassword.html*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-195">*resetpassword.html*</span></span> | <span data-ttu-id="bdaaf-196">암호 찾기 페이지의 템플릿으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="bdaaf-197">*selfasserted.html*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-197">*selfasserted.html*</span></span> | <span data-ttu-id="bdaaf-198">소셜 계정 등록 페이지, 로컬 계정 등록 페이지 또는 로컬 계정 로그인 페이지의 템플릿으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="bdaaf-199">*unified.html*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-199">*unified.html*</span></span> | <span data-ttu-id="bdaaf-200">통합 등록 또는 로그인 페이지의 템플릿으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="bdaaf-201">*updateprofile.html*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-201">*updateprofile.html*</span></span> | <span data-ttu-id="bdaaf-202">프로필 업데이트 페이지의 템플릿으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="bdaaf-203">Hello에 [등록 또는 로그인 시 사용자 지정 정책 섹션은 수정](#modify-your-sign-up-or-sign-in-custom-policy), hello에 대 한 콘텐츠 정의 구성 `api.idpselections`합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-203">In hello [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured hello content definition for `api.idpselections`.</span></span> <span data-ttu-id="bdaaf-204">콘텐츠 정의 hello Azure AD B2C id 경험 프레임 워크와 해당 설명을 보려면에서 인식 하는 Id의 전체 집합 hello는 다음 표에 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-204">hello full set of content definition IDs that are recognized by hello Azure AD B2C identity experience framework and their descriptions are in hello following table:</span></span>

| <span data-ttu-id="bdaaf-205">콘텐츠 정의 ID</span><span class="sxs-lookup"><span data-stu-id="bdaaf-205">Content definition ID</span></span> | <span data-ttu-id="bdaaf-206">설명</span><span class="sxs-lookup"><span data-stu-id="bdaaf-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="bdaaf-207">*api.error*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-207">*api.error*</span></span> | <span data-ttu-id="bdaaf-208">**오류 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-208">**Error page**.</span></span> <span data-ttu-id="bdaaf-209">예외 또는 오류가 발생하면 이 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="bdaaf-210">*api.idpselections*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-210">*api.idpselections*</span></span> | <span data-ttu-id="bdaaf-211">**ID 공급자 선택 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-211">**Identity provider selection page**.</span></span> <span data-ttu-id="bdaaf-212">이 페이지에는 로그인 시 사용자 hello 공급자에서 선택할 수는 id의 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-212">This page contains a list of identity providers that hello user can choose from during sign-in.</span></span> <span data-ttu-id="bdaaf-213">이러한 옵션은 엔터프라이즈 ID 공급자, 소셜 ID 공급자(예: Facebook, Google+) 또는 로컬 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="bdaaf-214">*api.idpselections.signup*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="bdaaf-215">**등록을 위한 ID 공급자 선택 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="bdaaf-216">이 페이지에는 사용자 hello 공급자 등록 중에서 선택할 수는 id의 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-216">This page contains a list of identity providers that hello user can choose from during sign-up.</span></span> <span data-ttu-id="bdaaf-217">이러한 옵션은 엔터프라이즈 ID 공급자, 소셜 ID 공급자(예: Facebook, Google+) 또는 로컬 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="bdaaf-218">*api.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="bdaaf-219">**암호 찾기 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-219">**Forgot password page**.</span></span> <span data-ttu-id="bdaaf-220">이 페이지에서는 폼 hello 사용자 암호 재설정 tooinitiate 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-220">This page contains a form that hello user must complete tooinitiate a password reset.</span></span>  |
| <span data-ttu-id="bdaaf-221">*api.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="bdaaf-222">**로컬 계정 로그인 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-222">**Local account sign-in page**.</span></span> <span data-ttu-id="bdaaf-223">이메일 주소 또는 사용자 이름을 기반으로 하는 로컬 계정으로 로그인하기 위한 양식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="bdaaf-224">hello 폼에 텍스트 입력된 상자 및 암호 입력 상자가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-224">hello form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="bdaaf-225">*api.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="bdaaf-226">**로컬 계정 등록 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-226">**Local account sign-up page**.</span></span> <span data-ttu-id="bdaaf-227">이메일 주소 또는 사용자 이름을 기반으로 하는 로컬 계정을 등록하기 위한 양식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="bdaaf-228">hello 폼에 텍스트 입력된 상자, 암호 입력 상자, 라디오 단추, 단일 선택 드롭다운 목록 상자 및 확인란 여러 개 선택 등의 다양 한 입력된 컨트롤에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-228">hello form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="bdaaf-229">*api.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-229">*api.phonefactor*</span></span> | <span data-ttu-id="bdaaf-230">**Multi-Factor Authentication 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="bdaaf-231">등록 또는 로그인 중에 사용자가 이 페이지에서 텍스트 또는 음성을 사용하여 전화 번호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="bdaaf-232">*api.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-232">*api.selfasserted*</span></span> | <span data-ttu-id="bdaaf-233">**소셜 계정 등록 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-233">**Social account sign-up page**.</span></span> <span data-ttu-id="bdaaf-234">소셜 ID 공급자(예: Facebook 또는 Google+)에서 기존 계정을 사용하여 등록할 때 사용자가 완성해야 하는 등록 양식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="bdaaf-235">이 페이지는 hello 암호 입력 필드를 제외 하 고 소셜 계정 등록 페이지를 앞으로 유사한 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-235">This page is similar toohello preceding social account sign-up page, except for hello password entry fields.</span></span> |
| <span data-ttu-id="bdaaf-236">*api.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="bdaaf-237">**프로필 업데이트 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-237">**Profile update page**.</span></span> <span data-ttu-id="bdaaf-238">이 페이지는 사용자가 사용할 수 있는 tooupdate 자신의 프로필 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-238">This page contains a form that users can use tooupdate their profile.</span></span> <span data-ttu-id="bdaaf-239">이 페이지는 비슷한 toohello 소셜 계정 등록 페이지 hello 암호 입력 필드를 제외 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-239">This page is similar toohello social account sign-up page, except for hello password entry fields.</span></span> |
| <span data-ttu-id="bdaaf-240">*api.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="bdaaf-240">*api.signuporsignin*</span></span> | <span data-ttu-id="bdaaf-241">**통합 등록 또는 로그인 페이지**입니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="bdaaf-242">이 페이지는 모두 hello 등록 및 로그인의 엔터프라이즈 id 공급자, Facebook 또는 Google + 또는 로컬 계정 등과 같은 소셜 id 공급자를 사용할 수 있는 사용자를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-242">This page handles both hello sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="bdaaf-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bdaaf-243">Next steps</span></span>

<span data-ttu-id="bdaaf-244">사용자 지정할 수 있는 UI 요소에 대한 추가 정보는 [기본 제공 정책의 UI 사용자 지정을 위한 참조 가이드](active-directory-b2c-reference-ui-customization.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdaaf-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
