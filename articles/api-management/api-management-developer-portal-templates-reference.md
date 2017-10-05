---
title: "Azure API Management 개발자 포털 템플릿 | Microsoft Docs"
description: "Azure API Management에서 템플릿 집합을 사용하여 개발자 포털 페이지의 콘텐츠를 사용자 지정하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 5189f3d8-2a4c-4dc8-ab19-11c7df0114d4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dc3f32a3cff2e66a798bd8f6c19c6b56a47643ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-developer-portal-templates"></a><span data-ttu-id="781c3-103">Azure API Management 개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="781c3-103">Azure API Management Developer Portal Templates</span></span>
<span data-ttu-id="781c3-104">Azure API Management는 해당 콘텐츠를 구성하는 템플릿 집합을 사용하여 개발자 포털 페이지의 콘텐츠를 사용자 지정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="781c3-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="781c3-105">이러한 템플릿에서 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers) 및 제공된 지역화 [String 리소스](api-management-template-resources.md#strings), [Glyph 리소스](api-management-template-resources.md#glyphs) 및 [Page 컨트롤](api-management-page-controls.md)의 집합과 같은 선택한 편집기를 사용하여 필요에 따라 페이지 콘텐츠를 유연하게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="781c3-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="781c3-106">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](api-management-developer-portal-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="781c3-106">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  



  
##  <span data-ttu-id="781c3-107"><a name="DeveloperPortalTemplates"></a> 개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="781c3-107"><a name="DeveloperPortalTemplates"></a> Developer portal templates</span></span>  
  
-   [<span data-ttu-id="781c3-108">API</span><span class="sxs-lookup"><span data-stu-id="781c3-108">APIs</span></span>](api-management-api-templates.md)  
    -   [<span data-ttu-id="781c3-109">API 목록</span><span class="sxs-lookup"><span data-stu-id="781c3-109">API list</span></span>](api-management-api-templates.md#APIList)  
    -   [<span data-ttu-id="781c3-110">작업</span><span class="sxs-lookup"><span data-stu-id="781c3-110">Operation</span></span>](api-management-api-templates.md#Product)  
    -   [<span data-ttu-id="781c3-111">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="781c3-111">Code samples</span></span>](api-management-api-templates.md#CodeSamples)  
        -   [<span data-ttu-id="781c3-112">Curl</span><span class="sxs-lookup"><span data-stu-id="781c3-112">Curl</span></span>](api-management-api-templates.md#Curl)  
        -   [<span data-ttu-id="781c3-113">C#</span><span class="sxs-lookup"><span data-stu-id="781c3-113">C#</span></span>](api-management-api-templates.md#CSharp)  
        -   [<span data-ttu-id="781c3-114">Java</span><span class="sxs-lookup"><span data-stu-id="781c3-114">Java</span></span>](api-management-api-templates.md#Stub)  
        -   [<span data-ttu-id="781c3-115">JavaScript</span><span class="sxs-lookup"><span data-stu-id="781c3-115">JavaScript</span></span>](api-management-api-templates.md#JavaScript)  
        -   [<span data-ttu-id="781c3-116">Objective C</span><span class="sxs-lookup"><span data-stu-id="781c3-116">Objective C</span></span>](api-management-api-templates.md#ObjectiveC)  
        -   [<span data-ttu-id="781c3-117">PHP</span><span class="sxs-lookup"><span data-stu-id="781c3-117">PHP</span></span>](api-management-api-templates.md#PHP)  
        -   [<span data-ttu-id="781c3-118">Python</span><span class="sxs-lookup"><span data-stu-id="781c3-118">Python</span></span>](api-management-api-templates.md#Python)  
        -   [<span data-ttu-id="781c3-119">Ruby</span><span class="sxs-lookup"><span data-stu-id="781c3-119">Ruby</span></span>](api-management-api-templates.md#Ruby)  
-   [<span data-ttu-id="781c3-120">제품</span><span class="sxs-lookup"><span data-stu-id="781c3-120">Products</span></span>](api-management-product-templates.md)  
    -   [<span data-ttu-id="781c3-121">제품 목록</span><span class="sxs-lookup"><span data-stu-id="781c3-121">Product list</span></span>](api-management-product-templates.md#ProductList)  
    -   [<span data-ttu-id="781c3-122">제품</span><span class="sxs-lookup"><span data-stu-id="781c3-122">Product</span></span>](api-management-product-templates.md#Product)  
-   [<span data-ttu-id="781c3-123">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="781c3-123">Applications</span></span>](api-management-application-templates.md)  
    -   [<span data-ttu-id="781c3-124">응용 프로그램 목록</span><span class="sxs-lookup"><span data-stu-id="781c3-124">Application list</span></span>](api-management-application-templates.md#ProductList)  
    -   [<span data-ttu-id="781c3-125">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="781c3-125">Application</span></span>](api-management-application-templates.md#Application)  
-   [<span data-ttu-id="781c3-126">문제</span><span class="sxs-lookup"><span data-stu-id="781c3-126">Issues</span></span>](api-management-issue-templates.md)  
    -   [<span data-ttu-id="781c3-127">문제 목록</span><span class="sxs-lookup"><span data-stu-id="781c3-127">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
-   [<span data-ttu-id="781c3-128">사용자 프로필</span><span class="sxs-lookup"><span data-stu-id="781c3-128">User Profile</span></span>](api-management-user-profile-templates.md)  
    -   [<span data-ttu-id="781c3-129">프로필</span><span class="sxs-lookup"><span data-stu-id="781c3-129">Profile</span></span>](api-management-user-profile-templates.md#Profile)  
    -   [<span data-ttu-id="781c3-130">구독</span><span class="sxs-lookup"><span data-stu-id="781c3-130">Subscriptions</span></span>](api-management-user-profile-templates.md#Subscriptions)  
    -   [<span data-ttu-id="781c3-131">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="781c3-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
    -   [<span data-ttu-id="781c3-132">계정 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="781c3-132">Update account info</span></span>](api-management-user-profile-templates.md#UpdateAccountInfo)  
-   [<span data-ttu-id="781c3-133">페이지</span><span class="sxs-lookup"><span data-stu-id="781c3-133">Pages</span></span>](api-management-page-templates.md)  
    -   [<span data-ttu-id="781c3-134">로그인</span><span class="sxs-lookup"><span data-stu-id="781c3-134">Sign in</span></span>](api-management-page-templates.md#SignIn)  
    -   [<span data-ttu-id="781c3-135">등록</span><span class="sxs-lookup"><span data-stu-id="781c3-135">Sign up</span></span>](api-management-page-templates.md#SignUp)  
    -   [<span data-ttu-id="781c3-136">페이지를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="781c3-136">Page not found</span></span>](api-management-page-templates.md#PageNotFound)


## <a name="next-steps"></a><span data-ttu-id="781c3-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="781c3-137">Next steps</span></span>  
-   [<span data-ttu-id="781c3-138">템플릿 참조</span><span class="sxs-lookup"><span data-stu-id="781c3-138">Template reference</span></span>](api-management-developer-portal-templates-reference.md)  
-   [<span data-ttu-id="781c3-139">데이터 모델 참조</span><span class="sxs-lookup"><span data-stu-id="781c3-139">Data model reference</span></span>](api-management-template-data-model-reference.md)  
-   [<span data-ttu-id="781c3-140">페이지 컨트롤</span><span class="sxs-lookup"><span data-stu-id="781c3-140">Page controls</span></span>](api-management-page-controls.md)  
-   [<span data-ttu-id="781c3-141">템플릿 리소스</span><span class="sxs-lookup"><span data-stu-id="781c3-141">Template resources</span></span>](api-management-template-resources.md)