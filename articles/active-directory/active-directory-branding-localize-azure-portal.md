---
title: "Azure Active Directory에서 로그인 페이지에 언어별 회사 브랜딩 추가 | Microsoft Docs"
description: "언어별 회사 브랜딩 그림 및 텍스트를 Azure에 로그인 페이지에 추가하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="92fb9-103">Azure Active Directory에서 로그인 페이지에 언어별 회사 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="92fb9-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="92fb9-104">혼동을 피하기 위해 대부분의 회사는 관리하는 모든 웹 사이트 및 서비스에 일관된 모양과 느낌을 적용하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="92fb9-105">Azure Active Directory는 회사 로고 및 사용자 지정 색 구성표를 포함하도록 로그인 페이지의 외관을 사용자 지정하는 방식으로 이 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="92fb9-106">로그인 페이지는 Office 365 또는 Azure AD를 ID 공급자로 사용하는 기타 웹 기반 응용 프로그램에 로그인할 경우에 표시되는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="92fb9-107">자격 증명을 입력하려면 이 페이지와 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="92fb9-108">다른 언어에 대한 로그인 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="92fb9-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="92fb9-109">[로그인 페이지에 회사 브랜딩 추가](active-directory-branding-custom-signon-azure-portal.md)에 설명된 대로 사용자 지정 로그인 페이지를 이미 만든 경우 사용자 지정 로그인 페이지에 언어별 요소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="92fb9-110">기본 사용자 지정 가능 요소 집합으로 디렉터리당 하나의 로그인 페이지를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="92fb9-111">기본 페이지 요소 집합을 구성한 후 다른 로캘로 추가 버전을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="92fb9-112">다양한 요소를 적절히 조합하여 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-112">You can also mix and match various elements.</span></span> <span data-ttu-id="92fb9-113">예를 들어 다음과 같이 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-113">For example, you could:</span></span>

* <span data-ttu-id="92fb9-114">모든 문화권에 적용되는 기본 **로그인 페이지 이미지** 를 만든 다음 영어와 프랑스어에 대한 특정 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="92fb9-115">다른 모든 언어에 대해 기본 그림이 표시되는 반면 이 두 언어 중 하나로 브라우저를 설정하면 언어별 이미지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="92fb9-116">조직에 따라 다른 로고를 구성합니다(예: 일본어 또는 히브리어 버전).</span><span class="sxs-lookup"><span data-stu-id="92fb9-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="92fb9-117">관리 및 성능 이유로 다양한 언어 변형을 낮게 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="92fb9-118">**디렉터리에 회사 브랜딩을 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="92fb9-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="92fb9-119">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="92fb9-120">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="92fb9-122">**사용자 및 그룹** 블레이드에서 **회사 브랜딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="92fb9-123">**사용자 및 그룹 - 회사 브랜딩** 블레이드에서 **언어 추가** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![언어별 브랜딩 요소 추가](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="92fb9-125">사용자 지정할 요소를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="92fb9-126">모든 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-126">All elements are optional.</span></span>
6. <span data-ttu-id="92fb9-127">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-127">Click **Save**.</span></span>

<span data-ttu-id="92fb9-128">로그인 페이지 브랜딩의 변경 내용을 보려면 최대 1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92fb9-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92fb9-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="92fb9-129">Next steps</span></span>
[<span data-ttu-id="92fb9-130">로그인 페이지에 회사 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="92fb9-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
