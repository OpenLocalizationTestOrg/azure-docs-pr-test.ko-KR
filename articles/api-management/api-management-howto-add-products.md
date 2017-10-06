---
title: "aaaHow toocreate 하 고 Azure API 관리에서 제품 게시"
description: "자세한 내용은 방법 toocreate 하 고 Azure API 관리에서 제품을 게시 합니다."
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
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="4febe-103">어떻게 toocreate 하 고 Azure API 관리에서 제품 게시</span><span class="sxs-lookup"><span data-stu-id="4febe-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="4febe-104">Azure API 관리에서 제품으로 하나 이상의 Api 사용 할당량 및 hello 사용 약관을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="4febe-105">제품이 게시 되 면 개발자 toohello 제품을 구독 하 고 toouse hello 제품의 Api를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="4febe-106">hello 항목 가이드 toocreating 제품에서 API를 추가 하 고 개발자를 위한 게시를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="4febe-107"><a name="create-product"> </a>제품 만들기</span><span class="sxs-lookup"><span data-stu-id="4febe-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="4febe-108">작업 추가 되 고 hello 게시자 포털에서 tooan API를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="4febe-109">tooaccess 게시자 포털을 클릭 하 여 hello **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="4febe-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![게시자 포털][api-management-management-console]

> <span data-ttu-id="4febe-111">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="4febe-112">클릭 **제품** hello 메뉴 hello 왼쪽된 toodisplay hello에서 **제품** 페이지를 클릭 하 여 **제품 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![제품][api-management-products]

![새 제품][api-management-add-new-product]

<span data-ttu-id="4febe-115">Hello에 hello 제품에 대 한 설명이 포함 된 이름을 입력 **이름** 필드와 hello 제품 hello에 대 한 설명 **설명** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="4febe-116">API Management에서 제품은 **개방형** 또는 **보호된** 제품일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="4febe-117">보호 된 제품에 사용할 수 있습니다, 열려 있는 동안 구독된 toobefore 여야 합니다. 구독 없이 제품을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="4febe-118">확인 **구독 필요** toocreate 구독 필요로 하는 보호 된 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="4febe-119">Hello 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-119">This is hello default setting.</span></span>

<span data-ttu-id="4febe-120">확인 **구독 승인이 필요한** 관리자 tooreview을 수락 하거나 거부 구독에서 toothis 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="4febe-121">Hello 상자 선택 하지 않으면 자동으로 승인 구독 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="4febe-122">구독에 대 한 자세한 내용은 참조 하십시오. [구독자 tooa 제품][View subscribers tooa product]합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="4febe-123">tooallow 개발자 계정 toosubscribe 여러 번 toohello 제품 확인 hello **여러 구독을 허용할** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="4febe-124">이 확인란을 선택 하지 않으면 각 개발자 계정을 한 번 toohello 제품만를 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![무제한의 여러 구독][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="4febe-126">여러 동시 구독 toolimit hello 수 확인 hello **동시에 대 한 구독 수를 제한** 확인란을 선택 하 고 hello 구독 제한을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="4febe-127">다음 예제는 hello에서 동시 구독은 개발자 계정당 toofour를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![네 개의 여러 구독][api-management-four-multiple-subscriptions]

<span data-ttu-id="4febe-129">모든 새 제품 옵션이 구성 되 면 클릭 **저장** toocreate hello 새 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![제품][api-management-products-page]

> <span data-ttu-id="4febe-131">기본적으로 새로운 제품은 게시, 아니며 표시만 toohello **관리자** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="4febe-132">hello에 hello 제품 이름을 제품을 tooconfigure 클릭 **제품** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="4febe-133"><a name="add-apis"></a>Tooa 제품 Api 추가</span><span class="sxs-lookup"><span data-stu-id="4febe-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="4febe-134">hello **제품** 페이지에 구성에 대 한 링크를 4 개: **요약**, **설정**, **가시성**, 및  **구독자**합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="4febe-135">hello **요약** 탭은 하거나 수 있는 Api를 추가 하 고 게시 제품 게시를 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![요약][api-management-new-product-summary]

<span data-ttu-id="4febe-137">제품을 게시 하기 전에 필요한 tooadd 하나 이상의 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="4febe-138">toodo이를 클릭 하이 여 **추가 API tooproduct**합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-138">toodo this, click **Add API tooproduct**.</span></span>

![API 추가][api-management-add-apis-to-product]

<span data-ttu-id="4febe-140">Select hello 필요한 Api 및 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="4febe-141"><a name="add-description"></a>추가 설명 정보 tooa 제품</span><span class="sxs-lookup"><span data-stu-id="4febe-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="4febe-142">hello **설정을** 탭에서는 tooprovide hello 제품의 용도, hello에 대 한 액세스를 제공 하는 Api 등 기타 유용한 정보에 대 한 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="4febe-143">hello 콘텐츠는 hello API를 호출 하 고 일반 텍스트 또는 HTML 태그에 쓸 수 있는 hello 개발자를 대상 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![제품 설정][api-management-product-settings]

<span data-ttu-id="4febe-145">확인 **구독 필요** toocreate는 구독 toobe 사용 하거나 선택 취소를 해야 하는 보호 된 제품 hello 확인란 toocreate는 open 제품 구독 없이 호출 될 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="4febe-146">선택 **구독 승인이 필요한** toomanually 제품에서 제공 하는 모든 구독 요청을 승인 하려면.</span><span class="sxs-lookup"><span data-stu-id="4febe-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="4febe-147">기본적으로 모든 제품 구독은 자동으로 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="4febe-148">tooallow 개발자 계정 toosubscribe 여러 번 toohello 제품 확인 hello **여러 구독을 허용할** 확인란을 선택 하 고 필요에 따라 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="4febe-149">이 확인란을 선택 하지 않으면 각 개발자 계정을 한 번 toohello 제품만를 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="4febe-150">필요에 따라 hello 입력 **사용 약관** 구독자 순서 toouse hello 제품에 동의 해야 하는 hello 제품에 대 한 사용 조건 hello를 설명 하는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="4febe-151"><a name="publish-product"> </a>제품 게시</span><span class="sxs-lookup"><span data-stu-id="4febe-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="4febe-152">제품에 Api hello을 호출 하기 전에 hello 제품 게시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="4febe-153">Hello에 **요약** hello 제품에 대 한 탭을 클릭 **게시**, 클릭 하 고 **예, 게시** tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="4febe-154">이전에 게시 된 제품 private toomake 클릭 **게시 취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-154">toomake a previously published product private, click **Unpublish**.</span></span>

![제품 게시][api-management-publish-product]

## <span data-ttu-id="4febe-156"><a name="make-visible"></a>제품 표시 toodevelopers 확인</span><span class="sxs-lookup"><span data-stu-id="4febe-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="4febe-157">hello **가시성** 탭에서는 toochoose 어떤 역할이 hello 개발자 포털에서 수 toosee hello 제품 및 toohello 제품을 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![제품 표시][api-management-product-visiblity]

<span data-ttu-id="4febe-159">그룹에 hello 개발자를 위한 제품의 tooenable 또는 사용 안 함 표시 유형 확인 또는 hello hello 그룹 옆에 있는 확인란의 선택을 취소 및 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="4febe-160">자세한 내용은 참조 [Azure API 관리에서 사용 하 여 toocreate 그룹 toomanage 개발자 계정을 어떻게][How toocreate and use groups toomanage developer accounts in Azure API Management]합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="4febe-161"><a name="view-subscribers"></a>구독자 tooa 제품</span><span class="sxs-lookup"><span data-stu-id="4febe-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="4febe-162">hello **구독자** toohello 제품을 구독 하는 hello 개발자 탭에 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="4febe-163">hello 세부 정보 및 각 개발자에 대 한 설정을 볼 수 있습니다 hello 개발자의 이름을 클릭 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="4febe-164">이 예에서 없는 개발자 toohello 제품 아직 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-164">In this example no developers have yet subscribed toohello product.</span></span>

![개발자][api-management-developer-list]

## <span data-ttu-id="4febe-166"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="4febe-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="4febe-167">한 번 hello 필요한 Api가 추가 하 고 hello 제품이 게시 개발자 수 toohello 제품 구독 toocall hello Api를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febe-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="4febe-168">이러한 항목 및 고급 제품 구성을 설명하는 자습서에 대해서는 [AzureAPI Management에서 고급 제품 설정을 만들고 구성하는 방법][How create and configure advanced product settings in Azure API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4febe-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="4febe-169">제품 사용에 대 한 자세한 내용은 hello 다음 비디오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4febe-169">For more information about working with products, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
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


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
