---
title: "Azure API Management의 제품 템플릿 | Microsoft Docs"
description: "Azure API Management 개발자 포털에서 제품 페이지의 콘텐츠를 사용자 지정하는 방법을 알아봅니다."
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
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="5c3a4-103">Azure API Management의 제품 템플릿</span><span class="sxs-lookup"><span data-stu-id="5c3a4-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="5c3a4-104">Azure API Management는 해당 콘텐츠를 구성하는 템플릿 집합을 사용하여 개발자 포털 페이지의 콘텐츠를 사용자 지정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="5c3a4-105">이러한 템플릿에서 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers) 및 제공된 지역화 [String 리소스](api-management-template-resources.md#strings), [Glyph 리소스](api-management-template-resources.md#glyphs) 및 [Page 컨트롤](api-management-page-controls.md)의 집합과 같은 편집기를 사용하여 필요에 따라 페이지 콘텐츠를 유연하게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="5c3a4-106">이 섹션의 템플릿을 통해 개발자 포털에서 제품 페이지의 콘텐츠를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="5c3a4-107">제품 목록</span><span class="sxs-lookup"><span data-stu-id="5c3a4-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="5c3a4-108">제품</span><span class="sxs-lookup"><span data-stu-id="5c3a4-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="5c3a4-109">다음 문서에는 샘플 기본 템플릿이 포함되어 있지만 지속적인 향상으로 인해 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="5c3a4-110">원하는 개별 템플릿으로 이동하여 개발자 포털에서 라이브 기본 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="5c3a4-111">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="5c3a4-112"><a name="ProductList"></a> 제품 목록</span><span class="sxs-lookup"><span data-stu-id="5c3a4-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="5c3a4-113">**제품 목록** 템플릿을 통해 개발자 포털에서 제품 목록 페이지의 본문을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="5c3a4-114">![제품 목록](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="5c3a4-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5c3a4-115">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="5c3a4-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="5c3a4-116">컨트롤</span><span class="sxs-lookup"><span data-stu-id="5c3a4-116">Controls</span></span>  
 <span data-ttu-id="5c3a4-117">`Product list` 템플릿에서 다음 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5c3a4-118">페이징 컨트롤</span><span class="sxs-lookup"><span data-stu-id="5c3a4-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="5c3a4-119">검색 컨트롤</span><span class="sxs-lookup"><span data-stu-id="5c3a4-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="5c3a4-120">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="5c3a4-120">Data model</span></span>  
  
|<span data-ttu-id="5c3a4-121">속성</span><span class="sxs-lookup"><span data-stu-id="5c3a4-121">Property</span></span>|<span data-ttu-id="5c3a4-122">형식</span><span class="sxs-lookup"><span data-stu-id="5c3a4-122">Type</span></span>|<span data-ttu-id="5c3a4-123">설명</span><span class="sxs-lookup"><span data-stu-id="5c3a4-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5c3a4-124">페이징</span><span class="sxs-lookup"><span data-stu-id="5c3a4-124">Paging</span></span>|<span data-ttu-id="5c3a4-125">[페이징](api-management-template-data-model-reference.md#Paging) 엔터티.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="5c3a4-126">제품 컬렉션에 대한 페이징 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="5c3a4-127">필터링</span><span class="sxs-lookup"><span data-stu-id="5c3a4-127">Filtering</span></span>|<span data-ttu-id="5c3a4-128">[필터링](api-management-template-data-model-reference.md#Filtering) 엔터티.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="5c3a4-129">제품 목록 페이지에 대한 필터링 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="5c3a4-130">제품</span><span class="sxs-lookup"><span data-stu-id="5c3a4-130">Products</span></span>|<span data-ttu-id="5c3a4-131">[제품](api-management-template-data-model-reference.md#Product) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="5c3a4-132">현재 사용자에게 표시되는 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5c3a4-133">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="5c3a4-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="5c3a4-134"><a name="Product"></a> 제품</span><span class="sxs-lookup"><span data-stu-id="5c3a4-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="5c3a4-135">**제품** 템플릿을 통해 개발자 포털에서 제품 페이지의 본문을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="5c3a4-136">![개발자 포털 제품 페이지](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="5c3a4-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5c3a4-137">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="5c3a4-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="5c3a4-138">컨트롤</span><span class="sxs-lookup"><span data-stu-id="5c3a4-138">Controls</span></span>  
 <span data-ttu-id="5c3a4-139">`Product list` 템플릿에서 다음 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5c3a4-140">구독 단추</span><span class="sxs-lookup"><span data-stu-id="5c3a4-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="5c3a4-141">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="5c3a4-141">Data model</span></span>  
  
|<span data-ttu-id="5c3a4-142">속성</span><span class="sxs-lookup"><span data-stu-id="5c3a4-142">Property</span></span>|<span data-ttu-id="5c3a4-143">형식</span><span class="sxs-lookup"><span data-stu-id="5c3a4-143">Type</span></span>|<span data-ttu-id="5c3a4-144">설명</span><span class="sxs-lookup"><span data-stu-id="5c3a4-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5c3a4-145">제품</span><span class="sxs-lookup"><span data-stu-id="5c3a4-145">Product</span></span>|[<span data-ttu-id="5c3a4-146">제품</span><span class="sxs-lookup"><span data-stu-id="5c3a4-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="5c3a4-147">지정된 제품.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-147">The specified product.</span></span>|  
|<span data-ttu-id="5c3a4-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="5c3a4-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="5c3a4-149">부울</span><span class="sxs-lookup"><span data-stu-id="5c3a4-149">boolean</span></span>|<span data-ttu-id="5c3a4-150">현재 사용자가 이 제품을 구독하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="5c3a4-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="5c3a4-151">SubscriptionState</span></span>|<span data-ttu-id="5c3a4-152">number</span><span class="sxs-lookup"><span data-stu-id="5c3a4-152">number</span></span>|<span data-ttu-id="5c3a4-153">구독의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-153">The state of the subscription.</span></span> <span data-ttu-id="5c3a4-154">가능한 상태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="5c3a4-155">-   `0 - suspended` – 구독이 차단되고 구독자는 제품의 API를 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="5c3a4-156">-   `1 - active` – 구독이 활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="5c3a4-157">-   `2 - expired` - 구독이 만료 날짜에 도달되었고 비활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="5c3a4-158">-   `3 - submitted` - 구독 요청이 개발자에 의해 발생했지만 아직 승인 또는 거부되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="5c3a4-159">-   `4 - rejected` – 구독 요청이 관리자에 의해 거부되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="5c3a4-160">-   `5 - cancelled` - 구독이 개발자 또는 관리자에 의해 취소되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="5c3a4-161">제한</span><span class="sxs-lookup"><span data-stu-id="5c3a4-161">Limits</span></span>|<span data-ttu-id="5c3a4-162">array</span><span class="sxs-lookup"><span data-stu-id="5c3a4-162">array</span></span>|<span data-ttu-id="5c3a4-163">이 속성은 사용되지 않으며 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="5c3a4-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="5c3a4-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="5c3a4-165">부울</span><span class="sxs-lookup"><span data-stu-id="5c3a4-165">boolean</span></span>|<span data-ttu-id="5c3a4-166">[위임](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/)이 이 구독에 대해 활성화되었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="5c3a4-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="5c3a4-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="5c3a4-168">string</span><span class="sxs-lookup"><span data-stu-id="5c3a4-168">string</span></span>|<span data-ttu-id="5c3a4-169">위임을 사용하는 경우 위임된 구독 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="5c3a4-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="5c3a4-170">IsAgreed</span></span>|<span data-ttu-id="5c3a4-171">부울</span><span class="sxs-lookup"><span data-stu-id="5c3a4-171">boolean</span></span>|<span data-ttu-id="5c3a4-172">제품에 약관이 있는 경우 현재 사용자가 약관에 동의했는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="5c3a4-173">구독</span><span class="sxs-lookup"><span data-stu-id="5c3a4-173">Subscriptions</span></span>|<span data-ttu-id="5c3a4-174">[구독 요약](api-management-template-data-model-reference.md#SubscriptionSummary) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="5c3a4-175">제품에 대한 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="5c3a4-176">API</span><span class="sxs-lookup"><span data-stu-id="5c3a4-176">Apis</span></span>|<span data-ttu-id="5c3a4-177">[API](api-management-template-data-model-reference.md#API) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="5c3a4-178">이 제품의 API입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="5c3a4-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="5c3a4-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="5c3a4-180">부울</span><span class="sxs-lookup"><span data-stu-id="5c3a4-180">boolean</span></span>|<span data-ttu-id="5c3a4-181">현재 사용자가 구독 제한과 관련하여 이 제품을 구독할 수 있는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="5c3a4-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="5c3a4-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="5c3a4-183">부울</span><span class="sxs-lookup"><span data-stu-id="5c3a4-183">boolean</span></span>|<span data-ttu-id="5c3a4-184">현재 사용자가 허용 또는 허용되지 않는 여러 구독과 관련하여 이 제품을 구독할 수 있는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5c3a4-185">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="5c3a4-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="5c3a4-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c3a4-186">Next steps</span></span>
<span data-ttu-id="5c3a4-187">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](api-management-developer-portal-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c3a4-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>