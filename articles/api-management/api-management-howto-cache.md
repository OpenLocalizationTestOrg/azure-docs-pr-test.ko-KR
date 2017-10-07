---
title: "Azure API 관리에서 tooimprove 성능 캐싱 aaaAdd | Microsoft Docs"
description: "Tooimprove hello 대기 시간, 대역폭 소비 및 웹 서비스 API 관리 서비스 호출에 대 한 로드 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="ea9ef-103">Azure API 관리에서 캐싱 tooimprove 성능을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="ea9ef-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="ea9ef-104">응답 캐싱을 위해 API 관리의 작업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="ea9ef-105">응답 캐싱은 그다지 사용되지 않는 데이터에 대한 API 대기 시간, 대역폭 사용량 및 웹 서비스 부하를 상당히 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="ea9ef-106">이 가이드에서는 tooadd 응답 API에 대 한 캐싱 및 hello 샘플 에코 API 작업에 대 한 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="ea9ef-107">Hello 작업 동작의 개발자 포털 tooverify 캐싱 hello에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="ea9ef-108">정책 식을 사용하여 키별 캐싱 항목에 대한 자세한 내용은 [Azure API 관리에서 사용자 지정 캐싱](api-management-sample-cache-by-key.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ea9ef-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ea9ef-109">Prerequisites</span></span>
<span data-ttu-id="ea9ef-110">이 가이드의 단계를 다음 hello를 먼저 API 관리 서비스 인스턴스를 사용 하 여 API와 구성 된 제품 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="ea9ef-111">API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="ea9ef-112"><a name="configure-caching"> </a>캐싱을 위해 작업 구성</span><span class="sxs-lookup"><span data-stu-id="ea9ef-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="ea9ef-113">이 단계에서는 hello 캐싱 hello의 설정을 검토 하 **가져올 리소스 (캐시 됨)** hello 샘플 에코 API의 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="ea9ef-114">각 API 관리 서비스 인스턴스를 사용 하는 tooexperiment 및 API 관리에 대 한 자세한 내용은 수 있는 에코 API와 미리 구성 된 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="ea9ef-115">자세한 내용은 [Azure API Management 시작][Get started with Azure API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="ea9ef-116">시작 tooget 클릭 **게시자 포털** API 관리 서비스에 대 한 hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="ea9ef-117">API 관리 게시자 포털 toohello 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-117">This takes you toohello API Management publisher portal.</span></span>

![게시자 포털][api-management-management-console]

<span data-ttu-id="ea9ef-119">클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **에코 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![Echo API][api-management-echo-api]

<span data-ttu-id="ea9ef-121">Hello 클릭 **작업** 탭을 클릭 한 다음 hello **가져올 리소스 (캐시 됨)** hello에서 작업 **작업** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Echo API 작업][api-management-echo-api-operations]

<span data-ttu-id="ea9ef-123">Hello 클릭 **캐싱** 탭 tooview hello 캐싱이 작업에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![캐싱 탭][api-management-caching-tab]

<span data-ttu-id="ea9ef-125">작업의 경우 선택 hello tooenable 캐싱 **사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="ea9ef-126">이 예제에서는 캐싱이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="ea9ef-127">Hello hello 값에 따라 각 작업 응답은 입력 **쿼리 문자열 매개 변수에 따라 다름** 및 **Vary 헤더에 의해** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="ea9ef-128">쿼리 문자열 매개 변수 또는 헤더에 따라 여러 응답 toocache 하려는 경우에이 두 필드에 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="ea9ef-129">**기간** hello 캐시 된 응답의 hello 만료 간격을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="ea9ef-130">이 예제에서는 hello 간격은 **3600** (초)를 해당 tooone 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="ea9ef-131">첫 번째 요청 toohello hello이 예제에서 구성을 캐싱 hello를 사용 하 여 **가져올 리소스 (캐시 됨)** 작업이 hello 백 엔드 서비스에서 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="ea9ef-132">이 응답 캐시 됩니다, 키가 지정 된 hello 지정 된 헤더 및 쿼리 문자열 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="ea9ef-133">Toohello 작업 매개 변수를 일치 하는 hello 갖습니다 후속 호출 hello 캐시 기간 간격이 만료 될 때까지 반환 된 응답을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="ea9ef-134"><a name="caching-policies"></a>검토 hello 캐싱 정책</span><span class="sxs-lookup"><span data-stu-id="ea9ef-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="ea9ef-135">이 단계에서는 hello 캐싱 hello에 대 한 설정을 검토 **가져올 리소스 (캐시 됨)** hello 샘플 에코 API의 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="ea9ef-136">Hello에 대 한 작업에 대 한 캐싱 설정을 구성한 경우 **캐싱** 캐싱 탭 hello 작업에 대 한 정책을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="ea9ef-137">이러한 정책은 확인 및 hello 정책 편집기에서 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="ea9ef-138">클릭 **정책** hello에서 **API 관리** hello 왼쪽과 선택한 후에 메뉴 **에코 API (캐시 됨) 하는 리소스 가져오기 /** hello에서 **작업**드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![정책 범위 작업][api-management-operation-dropdown]

<span data-ttu-id="ea9ef-140">그러면이 작업에 대 한 hello 정책 hello 정책 편집기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-140">This displays hello policies for this operation in hello policy editor.</span></span>

![API 관리 정책 편집기][api-management-policy-editor]

<span data-ttu-id="ea9ef-142">이 작업에 대 한 hello 정책 정의 된 hello를 사용 하 여 검토 하는 hello 캐싱 구성을 정의 하는 hello 정책을 포함 **캐싱** hello 이전 단계에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="ea9ef-143">캐싱 정책을 hello 정책 편집기에서 변경 내용을 toohello hello에 반영 됩니다 **캐싱** 탭의 작업을 반대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="ea9ef-144"><a name="test-operation"></a>작업 호출 및 hello 캐싱을 테스트</span><span class="sxs-lookup"><span data-stu-id="ea9ef-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="ea9ef-145">toosee hello 동작에서 캐싱에서는 작업을 호출할 수 hello hello 개발자 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="ea9ef-146">클릭 **개발자 포털** hello 맨 위 오른쪽 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-146">Click **Developer portal** in hello top right menu.</span></span>

![개발자 포털][api-management-developer-portal-menu]

<span data-ttu-id="ea9ef-148">클릭 **Api** 에 최상위 메뉴 hello 선택한 후 **에코 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> <span data-ttu-id="ea9ef-150">구성 하는 하나의 API가 있는 경우 표시 tooyour 계정 Api를 클릭 한 다음 이동 직접 해당 API에 대 한 toohello 작업.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="ea9ef-151">선택 hello **가져올 리소스 (캐시 됨)** 작업과 클릭 **콘솔을 열고**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![콘솔 시작][api-management-open-console]

<span data-ttu-id="ea9ef-153">hello 콘솔 hello 개발자 포털에서 직접 tooinvoke 작업을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![콘솔][api-management-console]

<span data-ttu-id="ea9ef-155">Hello에 대 한 기본값을 유지 **param1** 및 **매개 변수 2가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="ea9ef-156">선택 hello hello에서 원하는 키 **구독 키** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="ea9ef-157">계정에 구독이 하나만 있는 경우 이미 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="ea9ef-158">입력 **sampleheader:value1** hello에 **요청 헤더** 입력란.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="ea9ef-159">클릭 **HTTP Get** hello 메모 응답 헤더를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="ea9ef-160">입력 **sampleheader:value2** hello에 **요청 헤더** 텍스트 상자 및 클릭 **HTTP Get**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="ea9ef-161">해당 hello 값을 기록해 둡니다 **sampleheader** 여전히 **value1** hello에 대 한 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="ea9ef-162">일부 다른 값을 사용 하 고는 hello hello 첫 번째 호출에서 캐시 된 응답이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="ea9ef-163">입력 **25** hello에 **매개 변수 2가** 필드를 선택한 다음 클릭 **HTTP Get**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="ea9ef-164">해당 hello 값을 기록해 둡니다 **sampleheader** hello에 대 한 응답은 이제 **value2**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="ea9ef-165">Hello 작업 결과 쿼리 문자열에 따라 키가 지정 된, 때문에 hello 이전 캐시 된 응답이 반환 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="ea9ef-166"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea9ef-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="ea9ef-167">캐싱 정책에 대 한 자세한 내용은 참조 [캐싱 정책을] [ Caching policies] hello에 [API 관리 정책 참조][API Management policy reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="ea9ef-168">정책 식을 사용하여 키별 캐싱 항목에 대한 자세한 내용은 [Azure API 관리에서 사용자 지정 캐싱](api-management-sample-cache-by-key.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea9ef-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
