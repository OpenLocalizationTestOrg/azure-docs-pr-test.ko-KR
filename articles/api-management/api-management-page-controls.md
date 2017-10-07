---
title: "API 관리 페이지 컨트롤 aaaAzure | Microsoft Docs"
description: "Azure API 관리에서 개발자 포털 서식 파일에서 사용 하기 위해 사용할 수 있는 hello 페이지 컨트롤에 알아봅니다."
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
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="3db99-103">Azure API Management 페이지 컨트롤</span><span class="sxs-lookup"><span data-stu-id="3db99-103">Azure API Management page controls</span></span>
<span data-ttu-id="3db99-104">Azure API 관리 hello 다음 hello 개발자 포털 서식 파일에서 사용 하기 위해 컨트롤을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="3db99-105">toouse 컨트롤을 위치에 배치할 원하는 hello hello 개발자 포털 서식 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="3db99-106">Hello 같은 일부 컨트롤 [앱 작업](#app-actions) hello 다음 예제에에서 나와 있는 것 처럼 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="3db99-107">hello 매개 변수에 대 한 hello 값 hello 서식 파일에 대 한 hello 데이터 모델의 일부로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="3db99-108">대부분의 경우에서에 붙여 넣기만 하면 hello 예제 각 컨트롤에 제공 toowork 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="3db99-109">Hello 매개 변수 값에 대 한 자세한 내용은 hello 컨트롤을 사용할 수 있는 각 템플릿에 대 한 모델 섹션에 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="3db99-110">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="3db99-111">개발자 포털 템플릿 페이지 컨트롤</span><span class="sxs-lookup"><span data-stu-id="3db99-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="3db99-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="3db99-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="3db99-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="3db99-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="3db99-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="3db99-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="3db99-115">providers</span><span class="sxs-lookup"><span data-stu-id="3db99-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="3db99-116">search-control</span><span class="sxs-lookup"><span data-stu-id="3db99-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="3db99-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="3db99-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="3db99-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="3db99-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="3db99-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="3db99-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="3db99-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="3db99-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="3db99-121">hello `app-actions` 컨트롤 hello 사용자 프로필 페이지 hello 개발자 포털에서 응용 프로그램 상호 작용 하기 위한 사용자 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="3db99-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span><span class="sxs-lookup"><span data-stu-id="3db99-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="3db99-123">사용 현황</span><span class="sxs-lookup"><span data-stu-id="3db99-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="3db99-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-124">Parameters</span></span>  
  
|<span data-ttu-id="3db99-125">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-125">Parameter</span></span>|<span data-ttu-id="3db99-126">설명</span><span class="sxs-lookup"><span data-stu-id="3db99-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="3db99-127">appId</span><span class="sxs-lookup"><span data-stu-id="3db99-127">appId</span></span>|<span data-ttu-id="3db99-128">hello 응용 프로그램의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="3db99-129">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="3db99-129">Developer portal templates</span></span>  
 <span data-ttu-id="3db99-130">hello `app-actions` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="3db99-131">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="3db99-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="3db99-132"><a name="basic-signin"></a>basic-signin</span><span class="sxs-lookup"><span data-stu-id="3db99-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="3db99-133">hello `basic-signin` hello에 대 한 정보 수집 사용자 로그인 페이지 hello 개발자 포털에 로그인에 대 한 컨트롤은 컨트롤을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="3db99-134">![basic&#45;signin 컨트롤](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="3db99-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="3db99-135">사용 현황</span><span class="sxs-lookup"><span data-stu-id="3db99-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="3db99-136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-136">Parameters</span></span>  
 <span data-ttu-id="3db99-137">없음.</span><span class="sxs-lookup"><span data-stu-id="3db99-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="3db99-138">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="3db99-138">Developer portal templates</span></span>  
 <span data-ttu-id="3db99-139">hello `basic-signin` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="3db99-140">로그인</span><span class="sxs-lookup"><span data-stu-id="3db99-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="3db99-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="3db99-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="3db99-142">hello `paging-control` 항목의 목록을 표시 하는 포털 페이지 개발자에서 페이징 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="3db99-143">![페이징 컨트롤](./media/api-management-page-controls/APIM-paging-control.png "APIM 페이징 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="3db99-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="3db99-144">사용 현황</span><span class="sxs-lookup"><span data-stu-id="3db99-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="3db99-145">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-145">Parameters</span></span>  
 <span data-ttu-id="3db99-146">없음.</span><span class="sxs-lookup"><span data-stu-id="3db99-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="3db99-147">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="3db99-147">Developer portal templates</span></span>  
 <span data-ttu-id="3db99-148">hello `paging-control` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="3db99-149">API 목록</span><span class="sxs-lookup"><span data-stu-id="3db99-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="3db99-150">문제 목록</span><span class="sxs-lookup"><span data-stu-id="3db99-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="3db99-151">제품 목록</span><span class="sxs-lookup"><span data-stu-id="3db99-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="3db99-152"><a name="providers"></a> 공급자</span><span class="sxs-lookup"><span data-stu-id="3db99-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="3db99-153">hello `providers` 컨트롤 hello 로그인 hello 개발자 포털에서 페이지의 인증 공급자 선택에 대 한 컨트롤을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="3db99-154">![공급자 컨트롤](./media/api-management-page-controls/APIM-providers-control.png "APIM 공급자 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="3db99-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="3db99-155">사용 현황</span><span class="sxs-lookup"><span data-stu-id="3db99-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="3db99-156">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-156">Parameters</span></span>  
 <span data-ttu-id="3db99-157">없음.</span><span class="sxs-lookup"><span data-stu-id="3db99-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="3db99-158">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="3db99-158">Developer portal templates</span></span>  
 <span data-ttu-id="3db99-159">hello `providers` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="3db99-160">로그인</span><span class="sxs-lookup"><span data-stu-id="3db99-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="3db99-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="3db99-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="3db99-162">hello `search-control` 포털 페이지 항목의 목록을 표시 하는 개발자에 검색 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="3db99-163">![검색 컨트롤](./media/api-management-page-controls/APIM-search-control.png "APIM 검색 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="3db99-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="3db99-164">사용 현황</span><span class="sxs-lookup"><span data-stu-id="3db99-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="3db99-165">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-165">Parameters</span></span>  
 <span data-ttu-id="3db99-166">없음.</span><span class="sxs-lookup"><span data-stu-id="3db99-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="3db99-167">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="3db99-167">Developer portal templates</span></span>  
 <span data-ttu-id="3db99-168">hello `search-control` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="3db99-169">API 목록</span><span class="sxs-lookup"><span data-stu-id="3db99-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="3db99-170">제품 목록</span><span class="sxs-lookup"><span data-stu-id="3db99-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="3db99-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="3db99-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="3db99-172">hello `sign-up` 컨트롤 hello 등록 hello 개발자 포털에서 페이지에서에서 사용자 프로필 정보를 수집 하기 위한 컨트롤을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="3db99-173">![등록&#45;컨트롤](./media/api-management-page-controls/APIM-sign-up-control.png "APIM 등록 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="3db99-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="3db99-174">사용 현황</span><span class="sxs-lookup"><span data-stu-id="3db99-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="3db99-175">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-175">Parameters</span></span>  
 <span data-ttu-id="3db99-176">없음.</span><span class="sxs-lookup"><span data-stu-id="3db99-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="3db99-177">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="3db99-177">Developer portal templates</span></span>  
 <span data-ttu-id="3db99-178">hello `sign-up` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="3db99-179">등록</span><span class="sxs-lookup"><span data-stu-id="3db99-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="3db99-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="3db99-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="3db99-181">hello `subscribe-button` 사용자 tooa 제품을 구독에 대 한 컨트롤을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="3db99-182">![subscribe&#45;button 컨트롤](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="3db99-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="3db99-183">사용 현황</span><span class="sxs-lookup"><span data-stu-id="3db99-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="3db99-184">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-184">Parameters</span></span>  
 <span data-ttu-id="3db99-185">없음.</span><span class="sxs-lookup"><span data-stu-id="3db99-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="3db99-186">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="3db99-186">Developer portal templates</span></span>  
 <span data-ttu-id="3db99-187">hello `subscribe-button` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="3db99-188">제품</span><span class="sxs-lookup"><span data-stu-id="3db99-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="3db99-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="3db99-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="3db99-190">hello `subscription-cancel` 컨트롤의 hello 사용자 프로필 페이지 hello 개발자 포털에서 구독 tooa 제품을 취소 하는 것에 대 한 컨트롤을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="3db99-191">![subscription&#45;cancel 컨트롤](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel 컨트롤")</span><span class="sxs-lookup"><span data-stu-id="3db99-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="3db99-192">사용 현황</span><span class="sxs-lookup"><span data-stu-id="3db99-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="3db99-193">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-193">Parameters</span></span>  
  
|<span data-ttu-id="3db99-194">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3db99-194">Parameter</span></span>|<span data-ttu-id="3db99-195">설명</span><span class="sxs-lookup"><span data-stu-id="3db99-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="3db99-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="3db99-196">subscriptionId</span></span>|<span data-ttu-id="3db99-197">hello 구독 toocancel의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="3db99-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="3db99-198">cancelUrl</span></span>|<span data-ttu-id="3db99-199">hello 구독 URL을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="3db99-200">개발자 포털 템플릿</span><span class="sxs-lookup"><span data-stu-id="3db99-200">Developer portal templates</span></span>  
 <span data-ttu-id="3db99-201">hello `subscription-cancel` hello 개발자 포털 템플릿 다음에 제어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="3db99-202">제품</span><span class="sxs-lookup"><span data-stu-id="3db99-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="3db99-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3db99-203">Next steps</span></span>
<span data-ttu-id="3db99-204">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3db99-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
