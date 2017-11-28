---
title: "Azure API 관리에서 aaaProduct 템플릿 | Microsoft Docs"
description: "Hello 제품 toocustomize hello 콘텐츠 hello Azure API 관리 개발자 포털에서 페이지 하는 방식에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="28d78-103">Azure API Management의 제품 템플릿</span><span class="sxs-lookup"><span data-stu-id="28d78-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="28d78-104">Azure API 관리 개발자 포털 페이지 콘텐츠를 구성 하는 템플릿 집합을 사용 하 여 콘텐츠의 toocustomize hello 기능 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="28d78-105">사용 하 여 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 hello 편집기의 선택한와 같은 [디자이너에 대 한 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), 제공 된 집합을 지역화 [문자열 리소스](api-management-template-resources.md#strings), [ 문자 모양 리소스](api-management-template-resources.md#glyphs), 및 [컨트롤 페이지](api-management-page-controls.md), 이러한 템플릿을 사용 하 여 나타나며 hello 페이지의 뛰어난 유연성 tooconfigure hello 내용을 백업이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="28d78-106">이 섹션의 hello 템플릿을 hello 개발자 포털에서 toocustomize hello 내용의 hello 제품 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="28d78-107">제품 목록</span><span class="sxs-lookup"><span data-stu-id="28d78-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="28d78-108">제품</span><span class="sxs-lookup"><span data-stu-id="28d78-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="28d78-109">예제 기본 서식 파일 설명서, hello에 포함 되었지만 이러한 toocontinuous 개선 인해 주체 toochange 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="28d78-110">원하는 toohello 개별 서식 파일을 이동 하 여 hello 라이브 기본 템플릿 hello 개발자 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="28d78-111">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="28d78-112"><a name="ProductList"></a> 제품 목록</span><span class="sxs-lookup"><span data-stu-id="28d78-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="28d78-113">hello **제품 목록을** 템플릿을 사용 하 여 hello 제품 목록 페이지의 toocustomize hello 본문 hello 개발자 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="28d78-114">![제품 목록](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="28d78-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="28d78-115">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="28d78-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
        </li>     
    {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="28d78-116">컨트롤</span><span class="sxs-lookup"><span data-stu-id="28d78-116">Controls</span></span>  
 <span data-ttu-id="28d78-117">hello `Product list` 템플릿 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="28d78-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="28d78-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="28d78-119">검색 컨트롤</span><span class="sxs-lookup"><span data-stu-id="28d78-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="28d78-120">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="28d78-120">Data model</span></span>  
  
|<span data-ttu-id="28d78-121">속성</span><span class="sxs-lookup"><span data-stu-id="28d78-121">Property</span></span>|<span data-ttu-id="28d78-122">형식</span><span class="sxs-lookup"><span data-stu-id="28d78-122">Type</span></span>|<span data-ttu-id="28d78-123">설명</span><span class="sxs-lookup"><span data-stu-id="28d78-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="28d78-124">페이징</span><span class="sxs-lookup"><span data-stu-id="28d78-124">Paging</span></span>|<span data-ttu-id="28d78-125">[페이징](api-management-template-data-model-reference.md#Paging) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="28d78-126">hello hello 제품 컬렉션에 대 한 페이징 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="28d78-127">필터링</span><span class="sxs-lookup"><span data-stu-id="28d78-127">Filtering</span></span>|<span data-ttu-id="28d78-128">[필터링](api-management-template-data-model-reference.md#Filtering) 엔터티.</span><span class="sxs-lookup"><span data-stu-id="28d78-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="28d78-129">hello hello 제품 목록 페이지에 대 한 정보를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="28d78-130">제품</span><span class="sxs-lookup"><span data-stu-id="28d78-130">Products</span></span>|<span data-ttu-id="28d78-131">[제품](api-management-template-data-model-reference.md#Product) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="28d78-132">hello 제품 표시 toohello 현재 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="28d78-133">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="28d78-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="28d78-134"><a name="Product"></a> 제품</span><span class="sxs-lookup"><span data-stu-id="28d78-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="28d78-135">hello **제품** 템플릿을 사용 하 여 hello 제품 페이지 toocustomize hello 본문 hello 개발자 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="28d78-136">![개발자 포털 제품 페이지](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="28d78-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="28d78-137">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="28d78-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="28d78-138">컨트롤</span><span class="sxs-lookup"><span data-stu-id="28d78-138">Controls</span></span>  
 <span data-ttu-id="28d78-139">hello `Product list` 템플릿 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="28d78-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="28d78-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="28d78-141">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="28d78-141">Data model</span></span>  
  
|<span data-ttu-id="28d78-142">속성</span><span class="sxs-lookup"><span data-stu-id="28d78-142">Property</span></span>|<span data-ttu-id="28d78-143">형식</span><span class="sxs-lookup"><span data-stu-id="28d78-143">Type</span></span>|<span data-ttu-id="28d78-144">설명</span><span class="sxs-lookup"><span data-stu-id="28d78-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="28d78-145">제품</span><span class="sxs-lookup"><span data-stu-id="28d78-145">Product</span></span>|[<span data-ttu-id="28d78-146">제품</span><span class="sxs-lookup"><span data-stu-id="28d78-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="28d78-147">지정 된 제품 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-147">hello specified product.</span></span>|  
|<span data-ttu-id="28d78-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="28d78-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="28d78-149">부울</span><span class="sxs-lookup"><span data-stu-id="28d78-149">boolean</span></span>|<span data-ttu-id="28d78-150">여부 hello 현재 사용자는 구독 된 toothis 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="28d78-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="28d78-151">SubscriptionState</span></span>|<span data-ttu-id="28d78-152">number</span><span class="sxs-lookup"><span data-stu-id="28d78-152">number</span></span>|<span data-ttu-id="28d78-153">hello 구독의 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-153">hello state of hello subscription.</span></span> <span data-ttu-id="28d78-154">가능한 상태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="28d78-155">-   `0 - suspended`– hello 구독이 차단 되 고 hello 구독자 hello 제품의 Api를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="28d78-156">-   `1 - active`– hello 구독이 활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="28d78-157">-   `2 - expired`– hello 구독 만료 날짜에 도달 하 고 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="28d78-158">-   `3 - submitted`– hello 구독 요청이 hello 개발자가 이루어졌을 하지만 아직 승인 또는 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="28d78-159">-   `4 - rejected`– 관리자가 hello 구독 요청이 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="28d78-160">-   `5 - cancelled`– hello 개발자 또는 관리자가 hello 구독을 취소 했습니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="28d78-161">제한</span><span class="sxs-lookup"><span data-stu-id="28d78-161">Limits</span></span>|<span data-ttu-id="28d78-162">array</span><span class="sxs-lookup"><span data-stu-id="28d78-162">array</span></span>|<span data-ttu-id="28d78-163">이 속성은 사용되지 않으며 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="28d78-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="28d78-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="28d78-165">부울</span><span class="sxs-lookup"><span data-stu-id="28d78-165">boolean</span></span>|<span data-ttu-id="28d78-166">[위임](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/)이 이 구독에 대해 활성화되었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="28d78-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="28d78-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="28d78-168">string</span><span class="sxs-lookup"><span data-stu-id="28d78-168">string</span></span>|<span data-ttu-id="28d78-169">위임을 사용 하는 경우 구독 URL hello에 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="28d78-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="28d78-170">IsAgreed</span></span>|<span data-ttu-id="28d78-171">부울</span><span class="sxs-lookup"><span data-stu-id="28d78-171">boolean</span></span>|<span data-ttu-id="28d78-172">Hello 제품 용어 있으면 여부 hello 현재 사용자가 동의 toohello 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="28d78-173">구독</span><span class="sxs-lookup"><span data-stu-id="28d78-173">Subscriptions</span></span>|<span data-ttu-id="28d78-174">[구독 요약](api-management-template-data-model-reference.md#SubscriptionSummary) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="28d78-175">hello 구독 toohello 곱입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="28d78-176">API</span><span class="sxs-lookup"><span data-stu-id="28d78-176">Apis</span></span>|<span data-ttu-id="28d78-177">[API](api-management-template-data-model-reference.md#API) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="28d78-178">이 제품에 Api 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="28d78-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="28d78-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="28d78-180">부울</span><span class="sxs-lookup"><span data-stu-id="28d78-180">boolean</span></span>|<span data-ttu-id="28d78-181">Hello 현재 사용자 인지 여부와 관계 toohello 구독 제한 된 적격 toosubscribe toothis 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="28d78-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="28d78-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="28d78-183">부울</span><span class="sxs-lookup"><span data-stu-id="28d78-183">boolean</span></span>|<span data-ttu-id="28d78-184">Hello 현재 사용자가 적격 toosubscribe toothis 제품 허용 여부와 관계 toomultiple 구독과 인지 여부.</span><span class="sxs-lookup"><span data-stu-id="28d78-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="28d78-185">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="28d78-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="28d78-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28d78-186">Next steps</span></span>
<span data-ttu-id="28d78-187">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28d78-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
