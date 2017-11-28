---
title: "hello Azure Active Directory에서에서 tooyour 로그인 페이지 브랜딩 aaaAdd 언어별 회사 | Microsoft Docs"
description: "특정 언어 tooadd 회사 브랜딩 그림 및 텍스트 tooan Azure 로그인 페이지 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="71a9e-103">언어별 회사 hello Azure Active Directory에서에서 tooyour 로그인 페이지 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="71a9e-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="71a9e-104">tooavoid 혼동 많은 회사 모든 hello 웹 사이트 및 서비스 관리 tooapply 일관 된 모양과 느낌을 원합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="71a9e-105">Azure Active Directory 회사 로고 및 사용자 지정 색 구성표와 hello 로그인 페이지의 toocustomize hello 모양을 허용 하 여이 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="71a9e-106">hello 로그인 페이지에는 365 또는 id 공급자로 Azure AD를 사용 하는 다른 웹 기반 응용 프로그램 tooOffice에 로그인 할 때 표시 되는 hello 페이지가입니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="71a9e-107">자격 증명 페이지 tooenter이 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="71a9e-108">다른 언어에 대 한 hello 로그인 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="71a9e-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="71a9e-109">에 설명 된 대로 사용자 지정 로그인 페이지를 이미 만든 경우에 언어별로 요소 tooyour 사용자 지정 로그인 페이지를 추가할 수 있습니다 [회사 tooyour 로그인 페이지 브랜딩 추가](active-directory-branding-custom-signon-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="71a9e-110">기본 사용자 지정 가능 요소 집합으로 디렉터리당 하나의 로그인 페이지를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="71a9e-111">페이지 요소의 hello 기본 집합을 구성한 후에 각 로캘에 대해 더 많은 버전을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="71a9e-112">다양한 요소를 적절히 조합하여 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-112">You can also mix and match various elements.</span></span> <span data-ttu-id="71a9e-113">예를 들어 다음과 같이 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-113">For example, you could:</span></span>

* <span data-ttu-id="71a9e-114">모든 문화권에 적용되는 기본 **로그인 페이지 이미지** 를 만든 다음 영어와 프랑스어에 대한 특정 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="71a9e-115">이 두 언어의 브라우저 tooone 프로그램으로 설정 하면 다른 모든 언어에 대 한 hello 기본 그림이 표시 하는 동안 hello 언어별 이미지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="71a9e-116">조직에 따라 다른 로고를 구성합니다(예: 일본어 또는 히브리어 버전).</span><span class="sxs-lookup"><span data-stu-id="71a9e-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="71a9e-117">수 유지 하는 hello 다양 한 언어에 대 한 유지 관리와 성능상의 이유로 낮은 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="71a9e-118">**tooadd 회사 브랜딩 tooyour 디렉터리:**</span><span class="sxs-lookup"><span data-stu-id="71a9e-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="71a9e-119">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="71a9e-120">선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="71a9e-122">Hello에 **사용자 및 그룹** 블레이드를 **회사 브랜딩**합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="71a9e-123">Hello에 **사용자 및 그룹-회사 브랜딩** 블레이드, 선택 hello **언어 추가** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![언어별 브랜딩 요소 추가](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="71a9e-125">Toocustomize hello 요소를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="71a9e-126">모든 요소는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-126">All elements are optional.</span></span>
6. <span data-ttu-id="71a9e-127">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-127">Click **Save**.</span></span>

<span data-ttu-id="71a9e-128">변경한 모든 toohello 로그인 페이지 브랜딩 tooappear에 대 한 tooan 시간까지 걸릴 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a9e-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71a9e-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71a9e-129">Next steps</span></span>
[<span data-ttu-id="71a9e-130">회사 tooyour 로그인 페이지 브랜딩 추가</span><span class="sxs-lookup"><span data-stu-id="71a9e-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
