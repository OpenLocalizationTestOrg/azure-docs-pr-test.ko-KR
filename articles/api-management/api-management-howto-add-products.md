---
title: "Azure API 관리에서 제품을 만들고 게시하는 방법"
description: "Azure API 관리에서 제품을 만들고 게시하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="b23f0-103">Azure API 관리에서 제품을 만들고 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="b23f0-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="b23f0-104">Azure API 관리에서 제품은 하나 이상의 API뿐만 아니라 사용 할당량 및 사용 약관을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="b23f0-105">제품이 게시되면 개발자는 제품을 구독하고 제품의 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="b23f0-106">이 항목에서는 제품 생성, API 추가 및 개발자를 위한 게시를 안내해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="b23f0-107"><a name="create-product"> </a>제품 만들기</span><span class="sxs-lookup"><span data-stu-id="b23f0-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="b23f0-108">게시자 포털에서 작업을 API에 추가하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="b23f0-109">게시자 포털에 액세스하려면 API 관리 서비스에 대해 Azure Portal에서 **게시자 포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![게시자 포털][api-management-management-console]

> <span data-ttu-id="b23f0-111">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management 시작][Get started with Azure API Management] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b23f0-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="b23f0-112">왼쪽 메뉴에서 **제품**을 클릭하여 **제품** 페이지를 표시하고 **제품 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![제품][api-management-products]

![새 제품][api-management-add-new-product]

<span data-ttu-id="b23f0-115">**이름** 필드에 제품에 대한 설명적인 이름을 입력하고 **설명** 필드에 제품에 대한 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="b23f0-116">API Management에서 제품은 **개방형** 또는 **보호된** 제품일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="b23f0-117">보호된 제품은 사용하기 전에 구독해야 하는 반면, 개방형 제품은 구독하지 않고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="b23f0-118">**구독 필요** 를 선택하여 구독이 필요한 보호된 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="b23f0-119">기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-119">This is the default setting.</span></span>

<span data-ttu-id="b23f0-120">관리자가 이 제품에 대한 구독을 검토하고 허용하거나 거부하도록 하려면 **구독 승인 필요** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="b23f0-121">상자의 선택을 취소하면 구독 시도가 자동으로 승인됩니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="b23f0-122">구독에 대한 자세한 내용은 [제품 구독자 보기][View subscribers to a product]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b23f0-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="b23f0-123">개발자 계정으로 제품을 여러 번 구독할 수 있도록 하려면 **여러 구독 허용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="b23f0-124">이 확인란을 선택하지 않으면 각 개발자 계정은 제품을 한 번만 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![무제한의 여러 구독][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="b23f0-126">여러 동시 구독 수를 제한하려면 **동시 구독 제한 수** 확인란을 선택하고 구독 제한을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="b23f0-127">다음 예제에서는 동시 구독이 개발자 계정당 4개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![네 개의 여러 구독][api-management-four-multiple-subscriptions]

<span data-ttu-id="b23f0-129">새 제품 옵션을 모두 구성한 다음에는 **저장** 을 클릭하여 새 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![제품][api-management-products-page]

> <span data-ttu-id="b23f0-131">기본적으로 새 제품은 게시되지 않으며 **관리자** 그룹에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="b23f0-132">제품을 구성하려면 **제품** 탭에서 제품 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="b23f0-133"><a name="add-apis"> </a>제품에 여러 API 추가</span><span class="sxs-lookup"><span data-stu-id="b23f0-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="b23f0-134">**제품** 페이지에는 구성에 대한 4개의 링크인 **요약**, **설정**, **표시 여부** 및 **구독자** 링크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="b23f0-135">**요약** 탭에서는 API를 추가하고 제품을 게시하거나 게시를 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![요약][api-management-new-product-summary]

<span data-ttu-id="b23f0-137">제품을 게시하기 전에 API를 하나 이상 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="b23f0-138">이렇게 하려면 **제품에 API 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-138">To do this, click **Add API to product**.</span></span>

![API 추가][api-management-add-apis-to-product]

<span data-ttu-id="b23f0-140">원하는 API를 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="b23f0-141"><a name="add-description"> </a>제품에 설명 정보 추가</span><span class="sxs-lookup"><span data-stu-id="b23f0-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="b23f0-142">**설정** 탭에서 용도, 제품을 통해 액세스할 수 있는 API, 기타 유용한 정보 등의 자세한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="b23f0-143">콘텐츠는 API를 호출하는 개발자를 대상으로 하며 일반 텍스트 또는 HTML 표시로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![제품 설정][api-management-product-settings]

<span data-ttu-id="b23f0-145">**구독 필요** 를 선택하여 구독을 사용해야 하는 보호된 제품을 만들거나 확인란의 선택을 취소하여 구독 없이 호출할 수 있는 개방형 제품을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="b23f0-146">모든 제품 구독 요청을 수동으로 승인하려면 **구독 승인 필요** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="b23f0-147">기본적으로 모든 제품 구독은 자동으로 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="b23f0-148">개발자 계정으로 제품을 여러 번 구독할 수 있도록 하려면 확인은 **여러 구독 허용** 확인란을 선택하고 필요에 따라 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="b23f0-149">이 확인란을 선택하지 않으면 각 개발자 계정은 제품을 한 번만 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="b23f0-150">선택적으로 구독자가 제품을 사용하기 위해 허용해야 하는 제품의 사용 약관을 설명하는 **사용 약관** 필드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="b23f0-151"><a name="publish-product"> </a>제품 게시</span><span class="sxs-lookup"><span data-stu-id="b23f0-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="b23f0-152">제품의 API를 호출하려면 먼저 제품을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="b23f0-153">제품의 **요약** 탭에서 **게시**를 클릭한 다음 **예, 게시**를 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="b23f0-154">이전에 게시한 제품을 비공개로 설정하려면 **게시 취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-154">To make a previously published product private, click **Unpublish**.</span></span>

![제품 게시][api-management-publish-product]

## <span data-ttu-id="b23f0-156"><a name="make-visible"> </a>개발자에게 제품 표시</span><span class="sxs-lookup"><span data-stu-id="b23f0-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="b23f0-157">**표시** 탭에서, 개발자 포털의 제품을 보고 제품을 구독할 수 있는 역할을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![제품 표시][api-management-product-visiblity]

<span data-ttu-id="b23f0-159">그룹의 개발자에 대한 제품 표시를 사용하거나 사용하지 않으려면 그룹 옆에 있는 확인란을 선택하거나 선택 취소한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="b23f0-160">자세한 내용은 [Azure API Management에서 개발자 계정을 관리하는 그룹을 만들고 사용하는 방법][How to create and use groups to manage developer accounts in Azure API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b23f0-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="b23f0-161"><a name="view-subscribers"> </a>제품 구독자 보기</span><span class="sxs-lookup"><span data-stu-id="b23f0-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="b23f0-162">**구독자** 탭은 제품을 구독하는 개발자를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="b23f0-163">개발자 이름을 클릭하여 각 개발자에 대한 세부 정보 및 설정을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="b23f0-164">이 예제에서는 제품을 구독하는 개발자가 아직 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-164">In this example no developers have yet subscribed to the product.</span></span>

![개발자][api-management-developer-list]

## <span data-ttu-id="b23f0-166"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="b23f0-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="b23f0-167">원하는 API가 추가되고 제품이 게시되면 개발자는 제품을 구독하고 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b23f0-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="b23f0-168">이러한 항목 및 고급 제품 구성을 설명하는 자습서에 대해서는 [AzureAPI Management에서 고급 제품 설정을 만들고 구성하는 방법][How create and configure advanced product settings in Azure API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b23f0-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="b23f0-169">제품 사용에 대한 자세한 내용은 다음 비디오를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b23f0-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
