---
title: "Azure API Management 페이지 컨트롤 | Microsoft Docs"
description: "Azure API Management에서 개발자 포털 템플릿에 사용할 수 있는 페이지 컨트롤러에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="8c044-103">Azure API Management 페이지 컨트롤</span><span class="sxs-lookup"><span data-stu-id="8c044-103">Azure API Management page controls</span></span>
<span data-ttu-id="8c044-104">Azure API Management는 개발자 포털 템플릿에 사용할 수 있는 다음 컨트롤을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="8c044-105">컨트롤을 사용하려면 개발자 포털 템플릿의 원하는 위치에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="8c044-106">[app-actions](#app-actions) 컨트롤과 같은 일부 컨트롤에는 매개 변수가 있습니다(다음 예 참조).</span><span class="sxs-lookup"><span data-stu-id="8c044-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="8c044-107">매개 변수의 값은 템플릿에 대한 데이터 모델의 일부로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="8c044-108">대부분 경우 제대로 작동하도록 각 컨트롤에 대해 제공된 예제에 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="8c044-109">매개 변수 값에 대한 자세한 내용은 컨트롤을 사용할 수 있는 각 템플릿에 대한 데이터 모델 섹션을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="8c044-110">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c044-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="8c044-111">개발자 포털 템플릿 페이지 컨트롤</span><span class="sxs-lookup"><span data-stu-id="8c044-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="8c044-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="8c044-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="8c044-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="8c044-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="8c044-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="8c044-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="8c044-115">providers</span><span class="sxs-lookup"><span data-stu-id="8c044-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="8c044-116">search-control</span><span class="sxs-lookup"><span data-stu-id="8c044-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="8c044-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="8c044-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="8c044-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="8c044-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="8c044-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="8c044-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="8c044-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="8c044-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="8c044-121">`app-actions` 컨트롤은 개발자 포털의 사용자 프로필 페이지에서 응용 프로그램과 상호 작용하기 위한 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="8c044-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span><span class="sxs-lookup"><span data-stu-id="8c044-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8c044-123">사용 현황</span><span class="sxs-lookup"><span data-stu-id="8c044-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8c044-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-124">Parameters</span></span>  
  
|<span data-ttu-id="8c044-125">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-125">Parameter</span></span>|<span data-ttu-id="8c044-126">설명</span><span class="sxs-lookup"><span data-stu-id="8c044-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="8c044-127">appId</span><span class="sxs-lookup"><span data-stu-id="8c044-127">appId</span></span>|<span data-ttu-id="8c044-128">응용 프로그램의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8c044-129">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="8c044-129">Developer portal templates</span></span>  
 <span data-ttu-id="8c044-130">`app-actions` 컨트롤은 다음과 같은 개발자 포털 템플릿에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8c044-131">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8c044-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="8c044-132"><a name="basic-signin"></a>basic-signin</span><span class="sxs-lookup"><span data-stu-id="8c044-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="8c044-133">`basic-signin` 컨트롤은 개발자 포털의 로그인 페이지에서 사용자 로그인 정보를 수집하기 위한 컨트롤을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="8c044-134">![basic&#45;signin 컨트롤](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="8c044-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8c044-135">사용 현황</span><span class="sxs-lookup"><span data-stu-id="8c044-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8c044-136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-136">Parameters</span></span>  
 <span data-ttu-id="8c044-137">없음.</span><span class="sxs-lookup"><span data-stu-id="8c044-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8c044-138">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="8c044-138">Developer portal templates</span></span>  
 <span data-ttu-id="8c044-139">`basic-signin` 컨트롤은 다음과 같은 개발자 포털 템플릿에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8c044-140">로그인</span><span class="sxs-lookup"><span data-stu-id="8c044-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="8c044-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="8c044-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="8c044-142">`paging-control`은 개발자 포털 페이지에서 항목 목록을 표시하는 페이징 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="8c044-143">![페이징 컨트롤](./media/api-management-page-controls/APIM-paging-control.png "APIM 페이징 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="8c044-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8c044-144">사용 현황</span><span class="sxs-lookup"><span data-stu-id="8c044-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8c044-145">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-145">Parameters</span></span>  
 <span data-ttu-id="8c044-146">없음.</span><span class="sxs-lookup"><span data-stu-id="8c044-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8c044-147">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="8c044-147">Developer portal templates</span></span>  
 <span data-ttu-id="8c044-148">`paging-control` 컨트롤은 다음과 같은 개발자 포털 템플릿에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8c044-149">API 목록</span><span class="sxs-lookup"><span data-stu-id="8c044-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="8c044-150">문제 목록</span><span class="sxs-lookup"><span data-stu-id="8c044-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="8c044-151">제품 목록</span><span class="sxs-lookup"><span data-stu-id="8c044-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="8c044-152"><a name="providers"></a> 공급자</span><span class="sxs-lookup"><span data-stu-id="8c044-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="8c044-153">`providers` 컨트롤은 개발자 포털의 로그인 페이지에서 인증 공급자 선택을 위한 컨트롤을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="8c044-154">![공급자 컨트롤](./media/api-management-page-controls/APIM-providers-control.png "APIM 공급자 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="8c044-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8c044-155">사용 현황</span><span class="sxs-lookup"><span data-stu-id="8c044-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8c044-156">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-156">Parameters</span></span>  
 <span data-ttu-id="8c044-157">없음.</span><span class="sxs-lookup"><span data-stu-id="8c044-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8c044-158">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="8c044-158">Developer portal templates</span></span>  
 <span data-ttu-id="8c044-159">`providers` 컨트롤은 다음과 같은 개발자 포털 템플릿에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8c044-160">로그인</span><span class="sxs-lookup"><span data-stu-id="8c044-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="8c044-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="8c044-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="8c044-162">`search-control`은 개발자 포털 페이지에서 항목 목록을 표시하는 검색 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="8c044-163">![검색 컨트롤](./media/api-management-page-controls/APIM-search-control.png "APIM 검색 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="8c044-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8c044-164">사용 현황</span><span class="sxs-lookup"><span data-stu-id="8c044-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8c044-165">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-165">Parameters</span></span>  
 <span data-ttu-id="8c044-166">없음.</span><span class="sxs-lookup"><span data-stu-id="8c044-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8c044-167">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="8c044-167">Developer portal templates</span></span>  
 <span data-ttu-id="8c044-168">`search-control` 컨트롤은 다음과 같은 개발자 포털 템플릿에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8c044-169">API 목록</span><span class="sxs-lookup"><span data-stu-id="8c044-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="8c044-170">제품 목록</span><span class="sxs-lookup"><span data-stu-id="8c044-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="8c044-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="8c044-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="8c044-172">`sign-up` 컨트롤은 개발자 포털의 등록 페이지에서 사용자 프로필 정보를 수집하기 위한 컨트롤을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="8c044-173">![등록&#45;컨트롤](./media/api-management-page-controls/APIM-sign-up-control.png "APIM 등록 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="8c044-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8c044-174">사용 현황</span><span class="sxs-lookup"><span data-stu-id="8c044-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8c044-175">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-175">Parameters</span></span>  
 <span data-ttu-id="8c044-176">없음.</span><span class="sxs-lookup"><span data-stu-id="8c044-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8c044-177">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="8c044-177">Developer portal templates</span></span>  
 <span data-ttu-id="8c044-178">`sign-up` 컨트롤은 다음과 같은 개발자 포털 템플릿에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8c044-179">등록</span><span class="sxs-lookup"><span data-stu-id="8c044-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="8c044-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="8c044-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="8c044-181">`subscribe-button`은 사용자의 제품 구독에 대한 컨트롤을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="8c044-182">![subscribe&#45;button 컨트롤](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="8c044-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8c044-183">사용 현황</span><span class="sxs-lookup"><span data-stu-id="8c044-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="8c044-184">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-184">Parameters</span></span>  
 <span data-ttu-id="8c044-185">없음.</span><span class="sxs-lookup"><span data-stu-id="8c044-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8c044-186">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="8c044-186">Developer portal templates</span></span>  
 <span data-ttu-id="8c044-187">`subscribe-button` 컨트롤은 다음과 같은 개발자 포털 템플릿에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8c044-188">제품</span><span class="sxs-lookup"><span data-stu-id="8c044-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="8c044-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="8c044-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="8c044-190">`subscription-cancel` 컨트롤은 개발자 포털의 사용자 프로필 페이지에서 제품 구독 취소를 위한 컨트롤을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="8c044-191">![subscription&#45;cancel 컨트롤](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="8c044-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8c044-192">사용 현황</span><span class="sxs-lookup"><span data-stu-id="8c044-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="8c044-193">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-193">Parameters</span></span>  
  
|<span data-ttu-id="8c044-194">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8c044-194">Parameter</span></span>|<span data-ttu-id="8c044-195">설명</span><span class="sxs-lookup"><span data-stu-id="8c044-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="8c044-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="8c044-196">subscriptionId</span></span>|<span data-ttu-id="8c044-197">취소할 구독의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="8c044-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="8c044-198">cancelUrl</span></span>|<span data-ttu-id="8c044-199">구독 취소 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="8c044-200">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="8c044-200">Developer portal templates</span></span>  
 <span data-ttu-id="8c044-201">`subscription-cancel` 컨트롤은 다음과 같은 개발자 포털 템플릿에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c044-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="8c044-202">제품</span><span class="sxs-lookup"><span data-stu-id="8c044-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="8c044-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c044-203">Next steps</span></span>
<span data-ttu-id="8c044-204">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](api-management-developer-portal-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c044-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>