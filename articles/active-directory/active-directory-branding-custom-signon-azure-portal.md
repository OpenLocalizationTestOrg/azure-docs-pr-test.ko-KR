---
title: "페이지 hello Azure Active Directory에서에서 로그인에 aaaCustomize | Microsoft Docs"
description: "자세한 내용은 방법 tooadd 회사 브랜딩 toohello Azure 로그인 페이지"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="b4894-103">회사 hello Azure Active Directory에서에서 tooyour 로그인 페이지 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="b4894-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="b4894-104">tooavoid 혼동 많은 회사 모든 hello 웹 사이트 및 서비스 관리 tooapply 일관 된 모양과 느낌을 원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="b4894-105">Azure Active Directory 회사 로고 및 사용자 지정 색 구성표와 hello 로그인 페이지의 toocustomize hello 모양을 허용 하 여이 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="b4894-106">hello 로그인 페이지에는 365 또는 id 공급자로 Azure AD를 사용 하는 다른 웹 기반 응용 프로그램 tooOffice에 로그인 할 때 표시 되는 hello 페이지가입니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="b4894-107">자격 증명 페이지 tooenter이 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="b4894-108">회사 브랜드, 색 및이 페이지의 다른 사용자 지정 가능한 요소 tooshow를 원하는 경우 hello hello 두 환경 간의 이미지 toounderstand hello 차이 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b4894-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="b4894-109">다음 스크린 샷에 표시 및 데스크톱 컴퓨터에 Office 365 hello 로그인 페이지에 대 한 예제 hello **전에** 는 사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="b4894-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![사용자 지정하기 전 Office 365 로그인 페이지](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="b4894-111">다음 스크린 샷에 표시 및 데스크톱 컴퓨터에 Office 365 hello 로그인 페이지에 대 한 예제 hello **후** 는 사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="b4894-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![사용자 지정한 후 Office 365 로그인 페이지](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="b4894-113">Hello 로그인 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b4894-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="b4894-114">일반적으로 조직이 구독 하는 브라우저 기반 액세스 tooyour 클라우드 앱과 서비스를 필요 하면 hello 로그인 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="b4894-115">변경 내용 tooyour 로그인 페이지를 적용 한 경우 변경 내용 tooappear hello에 대 한 tooan 시간까지 걸릴 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="b4894-116">https://outlook.com/**contoso**.com 또는 https://mail.**contoso**.com과 같은 테넌트 특정 URL로 서비스를 이용할 경우 브랜드가 지정된 로그인 페이지만이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="b4894-117">비테넌트 특정 URL (예: https://mail.office365.com ) 을 사용하여 서비스에 방문하는 경우 브랜드가 지정되지 않은 로그인 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="b4894-118">이 경우에 사용자 ID를 입력하거나 사용자 타일을 선택하면 브랜딩이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="b4894-119">Hello에 도메인 이름이 "활성"으로 표시 해야 **도메인** 부분의 hello를 브랜딩을 구성한 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="b4894-120">자세한 내용은 [사용자 지정 도메인 이름 추가](active-directory-domains-add-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4894-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="b4894-121">로그인 페이지 브랜딩 toohello 소비자 로그인 페이지의 Microsoft 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="b4894-122">Microsoft 계정으로 로그인 하는 경우 Azure AD를 통해 렌더링 된 사용자 타일의 브랜드가 지정 된 목록이 표시 될 수 있지만 조직의 hello 브랜딩 toohello Microsoft 계정 로그인 페이지는 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="b4894-123">로그인 페이지에 hello **로그인 상태 유지** 확인란을 사용 하는 사용자 tooremain 닫고 브라우저를 다시 열 때 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![로그인 유지](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="b4894-125">세션 수명에는 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-125">It does not effect session lifetime.</span></span> <span data-ttu-id="b4894-126">Hello Azure Active Directory 로그인 페이지 hello 확인란을 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="b4894-127">hello 설정에 따라 hello 확인란이 표시 되는 여부 **사용 안 함에**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![로그인 유지](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="b4894-129">toohide hello 확인란, 너무이 설정을 구성 하**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="b4894-130">SharePoint Online 및 Office 2010의 일부 기능은이 상자 toocheck 수 있는 사용자가에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="b4894-131">이 설정은 toohidden를 구성 하면 toosign 기능을 추가 및 예기치 않은 메시지가 나타나면 사용자가 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="b4894-132">**tooadd 회사 브랜딩 tooyour 디렉터리:**</span><span class="sxs-lookup"><span data-stu-id="b4894-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="b4894-133">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="b4894-134">선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="b4894-136">Hello에 **사용자 및 그룹** 블레이드를 **회사 브랜딩**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="b4894-137">Hello에 **사용자 및 그룹-회사 브랜딩** 블레이드, 선택 hello **편집** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![사용자 지정 브랜딩 편집](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="b4894-139">Toocustomize hello 요소를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="b4894-140">모든 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-140">All elements are optional.</span></span>
6. <span data-ttu-id="b4894-141">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-141">Click **Save**.</span></span>

<span data-ttu-id="b4894-142">변경한 모든 toohello 로그인 페이지 브랜딩 tooappear에 대 한 tooan 시간까지 걸릴 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4894-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4894-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4894-143">Next steps</span></span>
[<span data-ttu-id="b4894-144">언어별 회사 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="b4894-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
