---
title: "Azure API 관리에서 API에 작업을 추가하는 방법 | Microsoft Docs"
description: "Azure API 관리에서 API에 작업을 추가하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 105fc51c2d1152a40a5757985da47330e0b7b8cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-operations-to-an-api-in-azure-api-management"></a><span data-ttu-id="99163-103">Azure API 관리에서 API에 작업을 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="99163-103">How to add operations to an API in Azure API Management</span></span>
<span data-ttu-id="99163-104">API 관리에서 API를 사용하려면 먼저 작업을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="99163-105">이 가이드에서는 API 관리에서 다양한 유형의 작업을 API에 추가하고 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="99163-105">This guide shows how to add and configure different types of operations to an API in API Management.</span></span>

## <span data-ttu-id="99163-106"><a name="add-operation"> </a>작업 추가</span><span class="sxs-lookup"><span data-stu-id="99163-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="99163-107">게시자 포털에서 작업을 API에 추가하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-107">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="99163-108">게시자 포털에 액세스하려면 API 관리 서비스에 대해 Azure Portal에서 **게시자 포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-108">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![게시자 포털][api-management-management-console]

> <span data-ttu-id="99163-110">아직 API Management 서비스 인스턴스를 만들지 않은 경우 [Azure API Management 시작][Get started with Azure API Management] 자습서의 [API Management 서비스 인스턴스 만들기][Create an API Management service instance]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99163-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="99163-111">게시자 포털에서 원하는 API를 선택한 다음 **작업** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-111">Select the desired API in the publisher portal and then select the **Operations** tab.</span></span> 

![작업][api-management-operations]

<span data-ttu-id="99163-113">새 작업을 추가하려면 **작업 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-113">Click **Add Operation** to add a new operation.</span></span> <span data-ttu-id="99163-114">**새 작업**이 표시되고 **서명** 탭이 기본으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="99163-114">The **New operation** will be displayed and the **Signature** tab will be selected by default.</span></span>

![작업 추가][api-management-add-operation]

<span data-ttu-id="99163-116">드롭다운 목록에서 **HTTP 동사** 를 선택하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-116">Specify the **HTTP verb** by choosing from the drop-down list.</span></span>

![HTTP 메서드][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="99163-118">하나 이상의 URL 경로 세그먼트 및 0개 이상의 쿼리 문자열 매개 변수로 구성된 URL 조각을 입력하여 URL 템플릿을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-118">Define the URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="99163-119">API의 기준 URL에 추가되는 URL 템플릿은 단일 HTTP 작업을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-119">The URL template, appended to the base URL of the API, identifies a single HTTP operation.</span></span> <span data-ttu-id="99163-120">여기에는 둥근 괄호로 식별되는 하나 이상의 명명된 변수 부분을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="99163-121">이러한 변수 부분을 템플릿 매개 변수라고 하며 요청을 API 관리 플랫폼으로 처리할 때 요청의 URL에서 추출하여 동적으로 할당되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="99163-121">These variable parts are called template parameters and are dynamically assigned values extracted from the request's URL when the request is being processed by the API Management platform.</span></span>

> <span data-ttu-id="99163-122">URL 템플릿은 와일드 카드 패턴을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-122">The URL template can include wildcard patterns.</span></span> <span data-ttu-id="99163-123">예를 들어 `/*`를 지정하면 해당 HTTP 메서드에 대한 모든 요청을 백 엔드 서비스로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-123">For example, specifying `/*` will forward all requests for that HTTP method to the back end service.</span></span>

![URL 템플릿][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="99163-125">필요한 경우 **URL 템플릿 다시 쓰기**를 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="99163-125">If desired, specify the **Rewrite URL template**.</span></span> <span data-ttu-id="99163-126">그렇게 하면 다시 쓰기 템플릿에 따라 변환된 URL을 통해 백 엔드를 호출하면서 프런트 엔드의 들어오는 요청을 처리하는 표준 URL 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-126">This allows you to use the standard URL template for processing incoming requests on the front-end, while calling the back-end via a converted URL according to the rewrite template.</span></span> <span data-ttu-id="99163-127">URL 템플릿의 템플릿 매개 변수는 다시 쓰기 템플릿에서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-127">Template parameters from the URL template should be used in the rewrite template.</span></span> <span data-ttu-id="99163-128">다음 예제에서는 위 예제에서 웹 서비스의 패스 세그먼트로 인코딩된 콘텐츠 유형을, URL 템플릿을 사용하여 API 관리 플랫폼을 통해 게시된 API에서 쿼리 매개 변수로 제공할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="99163-128">The following example shows how content type encoded as path segment in the web service from the previous example can be provided as a query parameter in the API published via the API Management platform using the URL templates.</span></span>

![URL 템플릿 다시 쓰기][api-management-url-template-rewrite]

<span data-ttu-id="99163-130">작업의 호출자는 `/customers?customerid=ALFKI` 형식을 사용하며 백 엔드 서비스를 호출할 때 이 형식은 `/Customers('ALFKI')`에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="99163-130">Callers to the operation will use the format `/customers?customerid=ALFKI` and this will be mapped to `/Customers('ALFKI')` when the back-end service is invoked.</span></span>

<span data-ttu-id="99163-131">**표시** 이름 및 **설명**은 작업에 대한 설명을 제공하며, 개발자 포털에서 API를 사용하는 개발자에게 문서를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="99163-131">**Display** name and **Description** provide a description of the operation and are used to provide documentation to the developers using this API in the developer portal.</span></span>

![설명][api-management-description]

<span data-ttu-id="99163-133">**설명** 입력란에 작업 설명을 일반 텍스트 또는 HTML로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-133">The operation description can be specified as plain text or HTML in the **Description** text box.</span></span>

## <span data-ttu-id="99163-134"><a name="operation-caching"> </a>작업 캐싱</span><span class="sxs-lookup"><span data-stu-id="99163-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="99163-135">응답 캐싱은 API 소비자에 인식되는 대기 시간을 줄이고, 대역폭 소비를 낮추고, API를 구현하는 HTTP 웹 서비스의 부하를 낮춥니다.</span><span class="sxs-lookup"><span data-stu-id="99163-135">Response caching reduces latency perceived by the API consumers, lowers bandwidth consumption and decreases the load on the HTTP web service implementing the API.</span></span> 

<span data-ttu-id="99163-136">작업에 대한 캐싱을 쉽고 빠르게 사용하려면 **캐싱** 탭을 선택하고 **사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-136">To easily and quickly enable caching for the operation, select the **Caching** tab and check the **Enable** checkbox.</span></span>

![구성][api-management-caching-tab]

<span data-ttu-id="99163-138">**기간** 은 작업 응답이 캐시에 남아 있는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-138">**Duration** specifies the time period during which the operation response remains in the cache.</span></span> <span data-ttu-id="99163-139">기본값은 3600초 또는 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="99163-139">The default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="99163-140">여러 캐시 키에 해당하는 응답이 별도의 캐시 값을 가져오도록 캐시 키는 응답 간을 구분하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="99163-140">Cache keys are used to differentiate between responses so that the response corresponding to each different cache key will get its own separate cached value.</span></span> <span data-ttu-id="99163-141">선택적으로, 각기 **쿼리 문자열 매개 변수에 따라 다름** 및 **헤더에 따라 다름** 입력란의 캐시 키 값을 계산하는 데 사용할 특정 쿼리 문자열 매개 변수 및/또는 HTTP 헤더를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-141">Optionally, enter specific query string parameters and/or HTTP headers to be used in computing cache key values in the **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="99163-142">아무것도 지정하지 않으면 전체 요청 URL과 HTTP 헤더 값 **Accept** 및 **Accept-Charset**가 캐시 키 생성에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="99163-142">When none are specified, full request URL and the following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="99163-143">캐싱 및 캐싱 정책에 대한 자세한 내용은 [Azure API 관리에서 작업 결과를 캐시하는 방법][How to cache operation results in Azure API Management]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99163-143">For more information on caching and caching policies, see [How to cache operation results in Azure API Management][How to cache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="99163-144"><a name="request-parameters"> </a>요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="99163-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="99163-145">작업 매개 변수는 매개 변수 탭에서 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-145">Operation parameters are managed on the Parameters tab.</span></span> <span data-ttu-id="99163-146">**서명** 탭의 **URL 템플릿**에 지정된 매개 변수는 자동으로 추가되며, URL 템플릿을 편집하여 이 매개 변수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-146">Parameters specified in the **URL Template** on the **Signature** tab are added automatically and can be changed only by editing the URL template.</span></span> <span data-ttu-id="99163-147">추가 매개 변수는 수동으로 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-147">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="99163-148">새 쿼리 매개 변수를 추가하려면 **쿼리 매개 변수 추가** 를 클릭하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-148">To add a new query parameter, click **Add Query Parameter** and enter the following information:</span></span>

* <span data-ttu-id="99163-149">**이름** - 매개 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="99163-149">**Name** - parameter name.</span></span>
* <span data-ttu-id="99163-150">**설명** - 매개 변수에 대한 짧은 설명입니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="99163-150">**Description** - a brief description of the parameter (optional).</span></span>
* <span data-ttu-id="99163-151">**유형** - 매개 변수 유형이며, 드롭다운에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-151">**Type** - parameter type, selected in the drop down.</span></span>
* <span data-ttu-id="99163-152">**값** - 이 매개 변수에 할당할 수 있는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="99163-152">**Values** - values that can be assigned to this parameter.</span></span> <span data-ttu-id="99163-153">값 중 하나를 기본값으로 표시할 수 있습니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="99163-153">One of the values can be marked as default (optional).</span></span>
* <span data-ttu-id="99163-154">**필수** - 확인란을 선택하여 매개 변수를 필수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-154">**Required** - make the parameter mandatory by checking the checkbox.</span></span> 

![요청 매개 변수][api-management-request-parameters]

## <span data-ttu-id="99163-156"><a name="request-body"> </a>요청 본문</span><span class="sxs-lookup"><span data-stu-id="99163-156"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="99163-157">작업에서 본문을 허용하거나(예: PUT, POST) 필요로 하는 경우 지원되는 모든 표시 형식(예: json, XML)으로 본문의 예제를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-157">If the operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of the supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="99163-158">요청 본문은 설명용으로만 제공될 뿐이며 유효성이 검증되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-158">The request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="99163-159">요청 본문을 입력하려면 **본문** 탭으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-159">To enter a request body, switch to the **Body** tab.</span></span>

<span data-ttu-id="99163-160">**표시 추가**를 클릭하고, 원하는 콘텐츠 형식 이름(예: 응용 프로그램/json)을 입력하고, 드롭다운에서 해당 이름을 선택하고, 선택한 형식의 필요한 요청 본문 예제를 입력란에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-160">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in the drop-down, and paste the desired request body example in the selected format into the text box.</span></span> 

![요청 본문][api-management-request-body]

<span data-ttu-id="99163-162">표시 외에도, **설명** 입력란에 설명을 선택적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-162">In additional to representations, you can also specify an optional text description in the **Description** text box.</span></span>

## <span data-ttu-id="99163-163"><a name="responses"> </a>응답</span><span class="sxs-lookup"><span data-stu-id="99163-163"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="99163-164">작업에서 생성될 수 있는 모든 상태 코드에 대한 응답 예제를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-164">It is a good practice to provide examples of responses for all status codes that the operation may produce.</span></span> <span data-ttu-id="99163-165">각 상태 코드에는 지원되는 콘텐츠 형식별로 하나씩, 두 개 이상의 응답 본문 예제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-165">Each status code may have more than one response body example, one for each of the supported content types.</span></span> 

<span data-ttu-id="99163-166">응답을 추가하려면 **추가** 를 클릭하고 원하는 상태 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-166">To add a response, click **Add** and start typing the desired status code.</span></span> <span data-ttu-id="99163-167">이 예제에서 상태 코드는 **200 OK**입니다.</span><span class="sxs-lookup"><span data-stu-id="99163-167">In this example the status code is **200 OK**.</span></span> <span data-ttu-id="99163-168">드롭다운에 표시되는 코드를 선택하면 응답 코드가 생성되어 작업에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="99163-168">Once the code is displayed in the drop-down, select it, and the response code is created and added to your operation.</span></span>

![응답 코드][api-management-response-code]

<span data-ttu-id="99163-170">**표시 추가**를 클릭하고, 원하는 콘텐츠 형식 이름(예: 응용 프로그램/json)을 입력한 다음, 드롭다운에서 해당 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-170">Click **Add Representation**, start typing the desired content type name (e.g. application/json) and then select it in the drop down.</span></span>

![본문 콘텐츠 형식][api-management-response-body-content-type]

<span data-ttu-id="99163-172">선택한 형식의 응답 본문 예제를 입력란에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="99163-172">Paste the response body example in the selected format into the text box.</span></span> 

![응답 본문][api-management-response-body]

<span data-ttu-id="99163-174">필요한 경우 **설명** 입력란에 선택적인 설명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-174">If desired, add an optional description into the **Description** text box.</span></span>

<span data-ttu-id="99163-175">작업이 구성되면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99163-175">Once the operation is configured, click **Save**.</span></span>

## <span data-ttu-id="99163-176"><a name="next-steps"> </a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="99163-176"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="99163-177">작업이 API에 추가되면 다음 단계는 제품과 API를 연결하고 개발자가 작업을 호출할 수 있도록 게시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="99163-177">Once the operations are added to an API, the next step is to associate the API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="99163-178">[제품을 만들고 게시하는 방법][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="99163-178">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
