---
title: "Azure Active Directory에서 로그인 페이지 사용자 지정 | Microsoft Docs"
description: "회사 브랜딩을 Azure 로그인 페이지 에 추가하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="361d2-103">Azure Active Directory에서 로그인 페이지에 회사 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="361d2-103">Add company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="361d2-104">혼동을 피하기 위해 대부분의 회사는 관리하는 모든 웹 사이트 및 서비스에 일관된 모양과 느낌을 적용하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="361d2-105">Azure Active Directory는 회사 로고 및 사용자 지정 색 구성표를 포함하도록 로그인 페이지의 외관을 사용자 지정하는 방식으로 이 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="361d2-106">로그인 페이지는 Office 365 또는 Azure AD를 ID 공급자로 사용하는 기타 웹 기반 응용 프로그램에 로그인할 경우에 표시되는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="361d2-107">자격 증명을 입력하려면 이 페이지와 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-107">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="361d2-108">이 페이지에 회사 브랜드, 색 및 기타 사용자지정 가능한 요소를 표시하려면 다음 이미지를 참조하여 두 환경의 차이를 이해하세요.</span><span class="sxs-lookup"><span data-stu-id="361d2-108">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="361d2-109">다음 스크린샷은 사용자 지정을 하기 **전에** 데스크톱 컴퓨터에서 Office 365 로그인 페이지에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-109">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![사용자 지정하기 전 Office 365 로그인 페이지](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="361d2-111">다음 스크린샷은 사용자 지정 **후** 데스크톱 컴퓨터 Office 365 로그인 페이지의 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-111">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![사용자 지정한 후 Office 365 로그인 페이지](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="361d2-113">로그인 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="361d2-113">Customizing the sign-in page</span></span>
<span data-ttu-id="361d2-114">일반적으로 조직이 구독하는 클라우드 앱 및 서비스에 대해 브라우저 기반 액세스가 필요한 경우 로그인 페이지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-114">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="361d2-115">로그인 페이지에 변경 내용을 적용할 경우 변경 내용을 표시하려면 최대 1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-115">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="361d2-116">https://outlook.com/**contoso**.com 또는 https://mail.**contoso**.com과 같은 테넌트 특정 URL로 서비스를 이용할 경우 브랜드가 지정된 로그인 페이지만이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="361d2-117">비테넌트 특정 URL (예: https://mail.office365.com ) 을 사용하여 서비스에 방문하는 경우 브랜드가 지정되지 않은 로그인 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="361d2-118">이 경우에 사용자 ID를 입력하거나 사용자 타일을 선택하면 브랜딩이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="361d2-119">도메인 이름은 브랜딩을 구성한 Azure 포털의 **도메인** 부분에서 "활성"으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-119">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="361d2-120">자세한 내용은 [사용자 지정 도메인 이름 추가](active-directory-domains-add-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="361d2-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="361d2-121">로그인 페이지 브랜딩은 Microsoft의 소비자 로그인 페이지에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-121">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="361d2-122">Microsoft 계정으로 로그인한 사용자는 Azure AD에서 렌더링하는 브랜드가 지정된 사용자 타일 목록을 볼 수 있지만 조직의 브랜딩이 Microsoft 계정 로그인 페이지에 적용되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="361d2-123">로그인 페이지의 **로그인 유지** 확인란은 사용자가 브라우저를 닫았다가 다시 열 때 로그인 상태를 유지할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-123">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![로그인 유지](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="361d2-125">세션 수명에는 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-125">It does not effect session lifetime.</span></span> <span data-ttu-id="361d2-126">이 확인란을 Azure Active Directory 로그인 페이지에서 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-126">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="361d2-127">확인란 표시 여부는 **로그인 상태 유지 사용 안 함** 설정에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-127">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![로그인 유지](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="361d2-129">확인란을 숨기려면 이 설정을 **예**로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-129">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="361d2-130">SharePoint Online과 Office 2010의 일부 기능은 이 확인란을 선택할 수 있는 사용자에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-130">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="361d2-131">이 설정을 숨겨짐으로 구성하면 사용자에게 로그인을 요청하는 예상치 못한 메시지가 추가로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-131">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="361d2-132">**디렉터리에 회사 브랜딩을 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="361d2-132">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="361d2-133">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-133">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="361d2-134">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-134">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="361d2-136">**사용자 및 그룹** 블레이드에서 **회사 브랜딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-136">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="361d2-137">**사용자 및 그룹 - 회사 브랜딩** 블레이드에서 **편집** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-137">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![사용자 지정 브랜딩 편집](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="361d2-139">사용자 지정할 요소를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-139">Modify the elements you want to customize.</span></span> <span data-ttu-id="361d2-140">모든 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-140">All elements are optional.</span></span>
6. <span data-ttu-id="361d2-141">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-141">Click **Save**.</span></span>

<span data-ttu-id="361d2-142">로그인 페이지 브랜딩의 변경 내용을 보려면 최대 1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="361d2-142">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="361d2-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="361d2-143">Next steps</span></span>
[<span data-ttu-id="361d2-144">언어별 회사 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="361d2-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
