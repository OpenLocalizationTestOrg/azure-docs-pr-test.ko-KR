---
title: "Azure Active Directory에서 로그인 페이지 사용자 지정 | Microsoft Docs"
description: "회사 브랜딩을 Azure 로그인 페이지 에 추가하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: bddf2542eecce8bdeccda6053203bf2c2ba0ffb2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="quickstart-add-company-branding-to-your-sign-in-page-in-azure-ad"></a><span data-ttu-id="8e833-103">빠른 시작: Azure AD에서 로그인 페이지에 회사 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="8e833-103">Quickstart: Add company branding to your sign-in page in Azure AD</span></span>
<span data-ttu-id="8e833-104">혼동을 피하기 위해 대부분의 회사는 관리하는 모든 웹 사이트 및 서비스에 일관된 모양과 느낌을 적용하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="8e833-105">Azure AD(Active Directory)는 회사 로고 및 사용자 지정 색 구성표를 포함하도록 로그인 페이지의 외관을 사용자 지정하는 방식으로 이 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-105">Azure Active Directory (Azure AD) provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="8e833-106">로그인 페이지는 Office 365 또는 Azure AD를 ID 공급자로 사용하는 기타 웹 기반 응용 프로그램에 로그인할 경우에 표시되는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="8e833-107">자격 증명을 입력하려면 이 페이지와 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-107">You interact with this page to enter your credentials.</span></span>

> [!NOTE]
> * <span data-ttu-id="8e833-108">회사 브랜딩은 Azure AD의 프리미엄 버전 또는 기본 버전으로 업그레이드하거나 Office 365 라이선스가 있는 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-108">Company branding is available only if you upgraded to the Premium or Basic edition of Azure AD, or have an Office 365 license.</span></span> <span data-ttu-id="8e833-109">기능이 라이선스 형식별로 지원되는지 알아보려면 [Azure Active Directory 가격 책정 정보 페이지](https://azure.microsoft.com/pricing/details/active-directory/)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="8e833-109">To learn if a feature is supported by your license type, check the [Azure Active Directory pricing information page](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>
> 
> * <span data-ttu-id="8e833-110">Azure Active Directory Premium 및 Basic 버전은 Azure Active Directory 전 세계 인스턴스를 사용하여 중국의 고객에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-110">Azure Active Directory Premium and Basic editions are available for customers in China using the worldwide instance of Azure Active Directory.</span></span> <span data-ttu-id="8e833-111">Azure Active Directory Premium 및 Basic 버전은 현재 중국 21Vianet이 운영하는 Microsoft Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-111">Azure Active Directory Premium and Basic editions are not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="8e833-112">자세한 내용은 [Azure Active Directory 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/)을 통해 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="8e833-112">For more information, contact us at the [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="8e833-113">로그인 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8e833-113">Customizing the sign-in page</span></span>

<!--You can customize the following elements on the sign-in page: <attach image>-->

<span data-ttu-id="8e833-114">사용자가 [*https://outlook.com/contoso.com*](https://outlook.com/contoso.com)과 같은 테넌트 관련 URL에 액세스할 때 회사 브랜딩 사용자 지정이 Azure AD 로그인 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-114">Company branding customizations appear on the Azure AD sign-in page when users access a tenant-specific URL such as [*https://outlook.com/contoso.com*](https://outlook.com/contoso.com).</span></span>

<span data-ttu-id="8e833-115">사용자가 www.office.com과 같은 일반 URL을 방문하면 시스템에서 사용자가 누구인지 인식할 수 없으므로 로그인 페이지에 회사 브랜딩 사용자 지정이 아직 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-115">When users visit a generic URL such as www.office.com, the sign-in page does not contain company branding customizations because the system doesn’t know who the user is.</span></span> <span data-ttu-id="8e833-116">사용자가 사용자 ID를 입력하거나 사용자 타일을 선택한 후에는 회사 브랜딩이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-116">Company branding will show after users enter their user ID or select a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="8e833-117">도메인 이름은 브랜딩을 구성한 Azure Portal의 **도메인** 부분에서 "활성"으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-117">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="8e833-118">자세한 내용은 [사용자 지정 도메인 이름 추가](add-custom-domain.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e833-118">For more information, see [Add a custom domain name](add-custom-domain.md).</span></span>
> * <span data-ttu-id="8e833-119">로그인 페이지 브랜딩은 개인 Microsoft 계정의 로그인 페이지에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-119">Sign-in page branding doesn’t carry over to the sign-in page for personal Microsoft accounts.</span></span> <span data-ttu-id="8e833-120">직원 또는 비즈니스 게스트가 개인 Microsoft 계정으로 로그인하는 경우 조직의 브랜딩이 로그인 페이지에 반영되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-120">If your employees or business guests sign in with a personal Microsoft account, their sign-in page does not reflect the branding of your organization.</span></span>


### <a name="banner-logo"></a><span data-ttu-id="8e833-121">배너 로고</span><span class="sxs-lookup"><span data-stu-id="8e833-121">Banner logo</span></span> 

<span data-ttu-id="8e833-122">설명</span><span class="sxs-lookup"><span data-stu-id="8e833-122">Description</span></span> | <span data-ttu-id="8e833-123">제약 조건</span><span class="sxs-lookup"><span data-stu-id="8e833-123">Constraints</span></span> | <span data-ttu-id="8e833-124">추천</span><span class="sxs-lookup"><span data-stu-id="8e833-124">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="8e833-125">배너 로고는 로그인 및 액세스 패널 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-125">The banner logo is displayed on the sign-in and the Access panel pages.</span></span><br><span data-ttu-id="8e833-126">로그인 페이지에서 사용자의 조직이 결정되면 일반적으로 사용자 이름을 입력한 후 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-126">On the sign-in page, this shows once the user’s organization is determined, usually after the username is entered.</span></span>  | <span data-ttu-id="8e833-127">투명 JPG 또는 PNG</span><span class="sxs-lookup"><span data-stu-id="8e833-127">Transparent JPG or PNG</span></span><br><span data-ttu-id="8e833-128">최대 높이: 36px</span><span class="sxs-lookup"><span data-stu-id="8e833-128">Max height: 36 px</span></span><br><span data-ttu-id="8e833-129">최대 너비: 245px</span><span class="sxs-lookup"><span data-stu-id="8e833-129">Max width: 245 px</span></span> | <span data-ttu-id="8e833-130">여기에서 조직의 로고를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-130">Use your organization’s logo here.</span></span><br><span data-ttu-id="8e833-131">투명 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-131">Use a transparent image.</span></span> <span data-ttu-id="8e833-132">배경이 흰색이 된다고 가정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="8e833-132">Don’t assume that the background will be white.</span></span><br><span data-ttu-id="8e833-133">이미지에서 로고 주위에 안쪽 여백을 추가하지 마십시오. 그렇지 않으면 로고가 불균형적으로 작게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-133">Do not add padding around your logo in the image or your logo will look disproportionately small.</span></span>

### <a name="username-hint"></a><span data-ttu-id="8e833-134">사용자 이름 힌트</span><span class="sxs-lookup"><span data-stu-id="8e833-134">Username hint</span></span>   
<span data-ttu-id="8e833-135">설명</span><span class="sxs-lookup"><span data-stu-id="8e833-135">Description</span></span> | <span data-ttu-id="8e833-136">제약 조건</span><span class="sxs-lookup"><span data-stu-id="8e833-136">Constraints</span></span> | <span data-ttu-id="8e833-137">추천</span><span class="sxs-lookup"><span data-stu-id="8e833-137">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="8e833-138">사용자 이름 필드의 힌트 텍스트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-138">This customizes the hint text in the username field.</span></span> | <span data-ttu-id="8e833-139">유니코드 텍스트 최대 64자</span><span class="sxs-lookup"><span data-stu-id="8e833-139">Unicode text up to 64 characters</span></span><br><span data-ttu-id="8e833-140">일반 텍스트 전용</span><span class="sxs-lookup"><span data-stu-id="8e833-140">Plain text only</span></span> | <span data-ttu-id="8e833-141">조직 외부의 게스트 사용자가 앱에 로그인하려면 이를 설정하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-141">We recommend that you do not set this if you expect guest users outside your organization to sign in to your app.</span></span>
            
### <a name="sign-in-page-text"></a><span data-ttu-id="8e833-142">로그인 페이지 텍스트</span><span class="sxs-lookup"><span data-stu-id="8e833-142">Sign-in page text</span></span>   
<span data-ttu-id="8e833-143">설명</span><span class="sxs-lookup"><span data-stu-id="8e833-143">Description</span></span> | <span data-ttu-id="8e833-144">제약 조건</span><span class="sxs-lookup"><span data-stu-id="8e833-144">Constraints</span></span> | <span data-ttu-id="8e833-145">추천</span><span class="sxs-lookup"><span data-stu-id="8e833-145">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="8e833-146">로그인 양식의 맨 아래에 표시되고 지원 센터에 대한 전화 번호 또는 법적 설명과 같은 추가 정보를 통신하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-146">This appears at the bottom of the sign-in form and can be used to communicate additional information such as the phone number to your help desk, or a legal statement.</span></span> | <span data-ttu-id="8e833-147">유니코드 텍스트 최대 256자</span><span class="sxs-lookup"><span data-stu-id="8e833-147">Unicode text up to 256 characters</span></span><br><span data-ttu-id="8e833-148">일반 텍스트 전용(링크 또는 HTML 태그 없음)</span><span class="sxs-lookup"><span data-stu-id="8e833-148">Plain text only (no links or HTML tags)</span></span>   

### <a name="sign-in-page-image"></a><span data-ttu-id="8e833-149">로그인 페이지 이미지</span><span class="sxs-lookup"><span data-stu-id="8e833-149">Sign-in page image</span></span>  
<span data-ttu-id="8e833-150">설명</span><span class="sxs-lookup"><span data-stu-id="8e833-150">Description</span></span> | <span data-ttu-id="8e833-151">제약 조건</span><span class="sxs-lookup"><span data-stu-id="8e833-151">Constraints</span></span> | <span data-ttu-id="8e833-152">추천</span><span class="sxs-lookup"><span data-stu-id="8e833-152">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="8e833-153">로그인 페이지의 배경에 표시되며 볼 수 있는 공간의 가운데에 고정되고 브라우저 창에 맞도록 크기 조정하고 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-153">This appears in the background of the sign-in page, is anchored to the center of the viewable space, and will scale and crop to fill the browser window.</span></span>    <br><span data-ttu-id="8e833-154">전화와 같은 좁은 화면에서는 이 이미지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-154">On narrow screens such as mobile phones, this image is not shown.</span></span><br><span data-ttu-id="8e833-155">0.55 불투명도의 검은색 마스크는 페이지가 로드될 때 코드에 의해 이 이미지 위에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-155">A black mask with 0.55 opacity will be applied over this image by our code when the page is loaded.</span></span> | <span data-ttu-id="8e833-156">JPG 또는 PNG</span><span class="sxs-lookup"><span data-stu-id="8e833-156">JPG or PNG</span></span><br><span data-ttu-id="8e833-157">이미지 크기: 1920x1080px</span><span class="sxs-lookup"><span data-stu-id="8e833-157">Image dimensions: 1920x1080 px</span></span><br><span data-ttu-id="8e833-158">파일 크기: &gt; 300KB</span><span class="sxs-lookup"><span data-stu-id="8e833-158">File size: &gt; 300 KB</span></span> | <br><span data-ttu-id="8e833-159">강력한 제목 포커스가 없는 곳에 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-159">Use images where there isn't a strong subject focus.</span></span> <span data-ttu-id="8e833-160">불투명 로그인 양식이 이 이미지의 가운데 위로 표시되고 브라우저 창 크기에 따라 이미지의 모든 부분을 덮을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-160">The opaque sign-in form appears over the center of this image and can cover any part of the image depending on the size of the browser window.</span></span><br><span data-ttu-id="8e833-161">빠른 로드 시간을 보장하려면 파일 크기를 가능한 한 작게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-161">Keep the file size as small as possible to ensure quick load times.</span></span> 

### <a name="background-color"></a><span data-ttu-id="8e833-162">배경색</span><span class="sxs-lookup"><span data-stu-id="8e833-162">Background Color</span></span>
<span data-ttu-id="8e833-163">설명</span><span class="sxs-lookup"><span data-stu-id="8e833-163">Description</span></span> | <span data-ttu-id="8e833-164">제약 조건</span><span class="sxs-lookup"><span data-stu-id="8e833-164">Constraints</span></span> | <span data-ttu-id="8e833-165">추천</span><span class="sxs-lookup"><span data-stu-id="8e833-165">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="8e833-166">낮은 대역폭 연결에서는 이 색이 배경 이미지 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-166">This color is used in place of the background image on low-bandwidth connections.</span></span> | <span data-ttu-id="8e833-167">16진수(예: #FFFFFF)의 RGB 색</span><span class="sxs-lookup"><span data-stu-id="8e833-167">RGB color in hexadecimal (example: #FFFFFF</span></span> | <span data-ttu-id="8e833-168">배너 로고 또는 조직 색의 기본 색을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-168">We suggest using the primary color of the banner logo or your organization color.</span></span>

### <a name="show-option-to-remain-signed-in"></a><span data-ttu-id="8e833-169">로그인 상태를 유지하는 옵션 표시</span><span class="sxs-lookup"><span data-stu-id="8e833-169">Show option to remain signed in</span></span>
<span data-ttu-id="8e833-170">설명</span><span class="sxs-lookup"><span data-stu-id="8e833-170">Description</span></span> | <span data-ttu-id="8e833-171">제약 조건</span><span class="sxs-lookup"><span data-stu-id="8e833-171">Constraints</span></span> | <span data-ttu-id="8e833-172">추천</span><span class="sxs-lookup"><span data-stu-id="8e833-172">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="8e833-173">Azure AD 로그인은 사용자가 브라우저를 닫고 다시 열 때 로그인 상태를 유지하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-173">Azure AD sign in gives the user the option to remain signed in when they close and re-open their browser.</span></span> <span data-ttu-id="8e833-174">이를 사용하여 해당 옵션을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-174">Use this to hide that option.</span></span><br><span data-ttu-id="8e833-175">이를 "아니요"로 설정하여 사용자에게 이 옵션을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-175">Set this to “No” to hide this option from your users.</span></span> | &nbsp; | <span data-ttu-id="8e833-176">세션 수명에는 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-176">This does not affect session lifetime.</span></span><br><span data-ttu-id="8e833-177">SharePoint Online과 Office 2010의 일부 기능은 로그인 상태를 유지하도록 선택할 수 있는 사용자에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-177">Some features of SharePoint Online and Office 2010 depend on users being able to choose to remain signed in.</span></span> <span data-ttu-id="8e833-178">이를 숨겨지도록 설정하면 사용자에게 로그인을 요청하는 예상치 못한 메시지가 추가로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-178">If you set this to be hidden, your users may see additional and unexpected prompts to sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="8e833-179">모든 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-179">All elements are optional.</span></span> <span data-ttu-id="8e833-180">예를 들어 배경 이미지가 없는 배너 로고를 지정하는 경우 로그인 페이지는 대상 사이트(예: Office 365)에 대한 로고 및 배경 이미지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-180">For example, if you specify a banner logo with no background image, the sign-in page will show your logo and the background image for the destination site (for example, Office 365).</span></span>

## <a name="add-company-branding-to-your-directory"></a><span data-ttu-id="8e833-181">디렉터리에 회사 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="8e833-181">Add company branding to your directory</span></span>

1. <span data-ttu-id="8e833-182">디렉터리에 대한 전역 관리자인 계정으로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-182">Sign in to [the Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="8e833-183">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-183">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="8e833-185">**사용자 및 그룹** 블레이드에서 **회사 브랜딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-185">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="8e833-186">**사용자 및 그룹 - 회사 브랜딩** 블레이드에서 **편집** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-186">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![사용자 지정 브랜딩 편집](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="8e833-188">사용자 지정할 요소를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-188">Modify the elements you want to customize.</span></span> <span data-ttu-id="8e833-189">모든 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-189">All elements are optional.</span></span>
6. <span data-ttu-id="8e833-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-190">Click **Save**.</span></span>

<span data-ttu-id="8e833-191">로그인 페이지 브랜딩의 변경 내용을 보려면 최대 1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-191">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="add-language-specific-company-branding-to-your-directory"></a><span data-ttu-id="8e833-192">디렉터리에 언어별 회사 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="8e833-192">Add language-specific company branding to your directory</span></span>

1. <span data-ttu-id="8e833-193">디렉터리에 대한 전역 관리자인 계정으로 [Azure AD 관리 센터](https://aad.portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-193">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="8e833-194">텍스트 상자에서 **사용자 및 그룹**을 선택한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-194">Select **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="8e833-196">**사용자 및 그룹** 블레이드에서 **회사 브랜딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-196">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="8e833-197">**사용자 및 그룹 - 회사 브랜딩** 블레이드에서 **언어 추가** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-197">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![언어별 브랜딩 요소 추가](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="8e833-199">사용자 지정할 요소를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-199">Modify the elements you want to customize.</span></span> <span data-ttu-id="8e833-200">모든 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-200">All elements are optional.</span></span>
6. <span data-ttu-id="8e833-201">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-201">Click **Save**.</span></span>

<span data-ttu-id="8e833-202">로그인 페이지 브랜딩의 변경 내용을 보려면 최대 1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-202">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e833-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e833-203">Next steps</span></span>
<span data-ttu-id="8e833-204">이 빠른 시작에서 Azure AD 디렉터리에 회사 브랜딩을 추가하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-204">In this quickstart, you’ve learned how to add company branding to your Azure AD directory.</span></span> 

<span data-ttu-id="8e833-205">다음 링크를 통해 Azure Portal에서 Azure AD에 회사 브랜딩을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e833-205">You can use the following link to configure your company branding in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8e833-206">회사 브랜딩 구성</span><span class="sxs-lookup"><span data-stu-id="8e833-206">Configure company branding</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 