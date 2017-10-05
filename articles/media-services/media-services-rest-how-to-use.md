---
title: "Media Services Operations REST API 개요 | Microsoft Docs"
description: "미디어 서비스 REST API 개요"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: eada8f2bcd2488d5ed36b0c24aa3d1b917815517
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-operations-rest-api-overview"></a><span data-ttu-id="780db-103">Media Services Operations REST API 개요</span><span class="sxs-lookup"><span data-stu-id="780db-103">Media Services operations REST API overview</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="780db-104">**Media Services Operations REST** API는 미디어 서비스 계정에서 작업, 자산, 액세스 정책 작성 및 개체에 대한 다른 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="780db-104">The **Media Services Operations REST** API is used for creating jobs, assets, access policies, and other operations on objects in a Media Service account.</span></span> <span data-ttu-id="780db-105">자세한 내용은 [Media Services Operations REST API 참조](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="780db-105">For more information, see [Media Services Operations REST API reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>

<span data-ttu-id="780db-106">Microsoft Azure 미디어 서비스는 OData 기반의 HTTP 요청을 허용하는 서비스이며 verbose JSON 또는 atom + pub 형식으로 다시 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780db-106">Microsoft Azure Media Services is a service that accepts OData-based HTTP requests and can respond back in verbose JSON or atom+pub.</span></span> <span data-ttu-id="780db-107">미디어 서비스는 Azure의 설계 지침을 따르기 때문에 미디어 서비스에 연결할 때 각 클라이언트가 사용해야 하는 필수 HTTP 헤더 집합뿐만 아니라 선택적 헤더로 사용할 수 있는 집합도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780db-107">Because Media Services conforms to Azure design guidelines, there is a set of required HTTP headers that each client must use when connecting to Media Services, as well as a set of optional headers that can be used.</span></span> <span data-ttu-id="780db-108">다음 섹션에서는 요청을 작성하고 미디어 서비스에서 응답을 수신할 때 사용할 수는 헤더 및 HTTP 동사를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-108">The following sections describe the headers and HTTP verbs you can use when creating requests and receiving responses from Media Services.</span></span>

<span data-ttu-id="780db-109">이 항목에서는 Media Services에서 REST v2를 사용하는 방법에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-109">This topic gives an overview of how to use REST v2 with Media Services.</span></span>

## <a name="considerations"></a><span data-ttu-id="780db-110">고려 사항</span><span class="sxs-lookup"><span data-stu-id="780db-110">Considerations</span></span>

<span data-ttu-id="780db-111">REST를 사용할 때 적용되는 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="780db-111">The following considerations apply when using REST.</span></span>

* <span data-ttu-id="780db-112">엔터티를 쿼리할 때 한 번에 반환되는 엔터티 수는 최대 1000개입니다. 공용 REST v2에서는 쿼리 결과를 1000개로 제한하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-112">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="780db-113">[이 .NET 예제](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) 및 [이 REST API 예제](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)에 설명된 대로 **Skip** 및 **Take**(.NET)/**top**(REST)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-113">You need to use **Skip** and **Take** (.NET)/ **top** (REST) as described in [this .NET example](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) and [this REST API example](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities).</span></span> 
* <span data-ttu-id="780db-114">JSON을 사용하고 요청(예: 연결된 개체 참조)에서 **__metadata** 키워드를 사용하도록 지정할 때 **Accept** 헤더를 [JSON 자세한 정보 표시 형식](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/)(아래 예제 참조)으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-114">When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object) you MUST set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (see the following example).</span></span> <span data-ttu-id="780db-115">verbose로 설정하지 않으면 Odata에서 **__metadata** 속성을 인식하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-115">Odata does not understand the **__metadata** property in the request, unless you set it to verbose.</span></span>  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a><span data-ttu-id="780db-116">미디어 서비스에서 지원하는 표준 HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="780db-116">Standard HTTP request headers supported by Media Services</span></span>
<span data-ttu-id="780db-117">미디어 서비스에서 작성한 모든 호출에는 귀하의 요청에 포함해야 하는 필수 헤더 집합이 있으며 포함할 수도 있는 선택적 헤더 집합도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780db-117">For every call you make into Media Services, there is a set of required headers you must include in your request and also a set of optional headers you may want to include.</span></span> <span data-ttu-id="780db-118">필수 헤더는 다음 표에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780db-118">The following table lists the required headers:</span></span>

| <span data-ttu-id="780db-119">헤더</span><span class="sxs-lookup"><span data-stu-id="780db-119">Header</span></span> | <span data-ttu-id="780db-120">형식</span><span class="sxs-lookup"><span data-stu-id="780db-120">Type</span></span> | <span data-ttu-id="780db-121">값</span><span class="sxs-lookup"><span data-stu-id="780db-121">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="780db-122">권한 부여</span><span class="sxs-lookup"><span data-stu-id="780db-122">Authorization</span></span> |<span data-ttu-id="780db-123">전달자</span><span class="sxs-lookup"><span data-stu-id="780db-123">Bearer</span></span> |<span data-ttu-id="780db-124">전달자는 승인된 유일한 권한 부여 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-124">Bearer is the only accepted authorization mechanism.</span></span> <span data-ttu-id="780db-125">이 값은 ACS에서 제공한 액세스 토큰도 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-125">The value must also include the access token provided by ACS.</span></span> |
| <span data-ttu-id="780db-126">x-ms-version</span><span class="sxs-lookup"><span data-stu-id="780db-126">x-ms-version</span></span> |<span data-ttu-id="780db-127">10진수</span><span class="sxs-lookup"><span data-stu-id="780db-127">Decimal</span></span> |<span data-ttu-id="780db-128">2.11</span><span class="sxs-lookup"><span data-stu-id="780db-128">2.11</span></span> |
| <span data-ttu-id="780db-129">DataServiceVersion</span><span class="sxs-lookup"><span data-stu-id="780db-129">DataServiceVersion</span></span> |<span data-ttu-id="780db-130">10진수</span><span class="sxs-lookup"><span data-stu-id="780db-130">Decimal</span></span> |<span data-ttu-id="780db-131">3.0</span><span class="sxs-lookup"><span data-stu-id="780db-131">3.0</span></span> |
| <span data-ttu-id="780db-132">MaxDataServiceVersion</span><span class="sxs-lookup"><span data-stu-id="780db-132">MaxDataServiceVersion</span></span> |<span data-ttu-id="780db-133">10진수</span><span class="sxs-lookup"><span data-stu-id="780db-133">Decimal</span></span> |<span data-ttu-id="780db-134">3.0</span><span class="sxs-lookup"><span data-stu-id="780db-134">3.0</span></span> |

> [!NOTE]
> <span data-ttu-id="780db-135">미디어 서비스는 OData를 사용하여 REST API를 통해 기본 자산 메타데이터 리포지토리를 표시합니다. DataServiceVersion과 MaxDataServiceVersion 헤더는 모든 요청에 포함되어야 합니다. 그러나 그렇지 않은 경우 현재 미디어 서비스는 사용 중인 DataServiceVersion 값이 3.0이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-135">Because Media Services uses OData to expose its underlying asset metadata repository through REST APIs, the DataServiceVersion and MaxDataServiceVersion headers should be included in any request; however, if they are not, then currently Media Services assumes the DataServiceVersion value in use is 3.0.</span></span>
> 
> 

<span data-ttu-id="780db-136">다음은 선택적 헤더의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-136">The following is a set of optional headers:</span></span>

| <span data-ttu-id="780db-137">헤더</span><span class="sxs-lookup"><span data-stu-id="780db-137">Header</span></span> | <span data-ttu-id="780db-138">형식</span><span class="sxs-lookup"><span data-stu-id="780db-138">Type</span></span> | <span data-ttu-id="780db-139">값</span><span class="sxs-lookup"><span data-stu-id="780db-139">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="780db-140">Date</span><span class="sxs-lookup"><span data-stu-id="780db-140">Date</span></span> |<span data-ttu-id="780db-141">RFC 1123 날짜</span><span class="sxs-lookup"><span data-stu-id="780db-141">RFC 1123 date</span></span> |<span data-ttu-id="780db-142">요청 타임스탬프</span><span class="sxs-lookup"><span data-stu-id="780db-142">Timestamp of the request</span></span> |
| <span data-ttu-id="780db-143">수락</span><span class="sxs-lookup"><span data-stu-id="780db-143">Accept</span></span> |<span data-ttu-id="780db-144">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="780db-144">Content type</span></span> |<span data-ttu-id="780db-145">다음과 같은 응답에 대해 요청된 콘텐츠 형식:</span><span class="sxs-lookup"><span data-stu-id="780db-145">The requested content type for the response such as the following:</span></span><p> <span data-ttu-id="780db-146">-application/json;odata=verbose</span><span class="sxs-lookup"><span data-stu-id="780db-146">-application/json;odata=verbose</span></span><p> <span data-ttu-id="780db-147">- application/atom+xml</span><span class="sxs-lookup"><span data-stu-id="780db-147">- application/atom+xml</span></span><p> <span data-ttu-id="780db-148">blob 인출과 같이 다른 콘텐츠 유형이 응답에 있을 수 있습니다. 여기서 성공적인 응답은 blob 스트림을 페이로드로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-148">Responses may have a different content type, such as a blob fetch, where a successful response will contain the blob stream as the payload.</span></span> |
| <span data-ttu-id="780db-149">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="780db-149">Accept-Encoding</span></span> |<span data-ttu-id="780db-150">Gzip, deflate</span><span class="sxs-lookup"><span data-stu-id="780db-150">Gzip, deflate</span></span> |<span data-ttu-id="780db-151">GZIP 및 DEFLATE 인코딩, 해당되는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-151">GZIP and DEFLATE encoding, when applicable.</span></span> <span data-ttu-id="780db-152">참고: 큰 리소스의 경우 미디어 서비스는 이 헤더를 무시하고 압축되지 않은 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780db-152">Note: For large resources, Media Services may ignore this header and return noncompressed data.</span></span> |
| <span data-ttu-id="780db-153">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="780db-153">Accept-Language</span></span> |<span data-ttu-id="780db-154">"en", "es" 등입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-154">"en", "es", and so on.</span></span> |<span data-ttu-id="780db-155">응답에 대한 기본 언어를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-155">Specifies the preferred language for the response.</span></span> |
| <span data-ttu-id="780db-156">Accept-Charset</span><span class="sxs-lookup"><span data-stu-id="780db-156">Accept-Charset</span></span> |<span data-ttu-id="780db-157">"UTF-8"과 같은 문자 집합 유형</span><span class="sxs-lookup"><span data-stu-id="780db-157">Charset type like “UTF-8”</span></span> |<span data-ttu-id="780db-158">기본값은 UTF-8입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-158">Default is UTF-8.</span></span> |
| <span data-ttu-id="780db-159">X-HTTP-Method</span><span class="sxs-lookup"><span data-stu-id="780db-159">X-HTTP-Method</span></span> |<span data-ttu-id="780db-160">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="780db-160">HTTP Method</span></span> |<span data-ttu-id="780db-161">PUT 또는 DELETE와 같이 HTTP 메서드를 지원하지 않는 클라이언트나 방화벽이 GET 호출을 통해 터널링된 이러한 메서드를 사용하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-161">Allows clients or firewalls that do not support HTTP methods like PUT or DELETE to use these methods, tunneled via a GET call.</span></span> |
| <span data-ttu-id="780db-162">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="780db-162">Content-Type</span></span> |<span data-ttu-id="780db-163">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="780db-163">Content type</span></span> |<span data-ttu-id="780db-164">PUT 또는 POST 요청에서 요청 본문의 콘텐츠 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-164">Content type of the request body in PUT or POST requests.</span></span> |
| <span data-ttu-id="780db-165">client-request-id</span><span class="sxs-lookup"><span data-stu-id="780db-165">client-request-id</span></span> |<span data-ttu-id="780db-166">String</span><span class="sxs-lookup"><span data-stu-id="780db-166">String</span></span> |<span data-ttu-id="780db-167">지정된 요청을 식별하는 호출자 정의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-167">A caller-defined value that identifies the given request.</span></span> <span data-ttu-id="780db-168">지정된 경우 이 값은 요청을 매핑하는 방법으로 응답 메시지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="780db-168">If specified, this value will be included in the response message as a way to map the request.</span></span> <p><p><span data-ttu-id="780db-169">**중요**</span><span class="sxs-lookup"><span data-stu-id="780db-169">**Important**</span></span><p><span data-ttu-id="780db-170">값은 2096b(2k)에서 제한되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-170">Values should be capped at 2096b (2k).</span></span> |

## <a name="standard-http-response-headers-supported-by-media-services"></a><span data-ttu-id="780db-171">미디어 서비스에서 지원되는 표준 HTTP 응답 헤더</span><span class="sxs-lookup"><span data-stu-id="780db-171">Standard HTTP response headers supported by Media Services</span></span>
<span data-ttu-id="780db-172">다음은 요청한 리소스 및 수행하려는 작업에 따라 사용자에게 반환될 수 있는 헤더 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-172">The following is a set of headers that may be returned to you depending on the resource you were requesting and the action you intended to perform.</span></span>

| <span data-ttu-id="780db-173">헤더</span><span class="sxs-lookup"><span data-stu-id="780db-173">Header</span></span> | <span data-ttu-id="780db-174">형식</span><span class="sxs-lookup"><span data-stu-id="780db-174">Type</span></span> | <span data-ttu-id="780db-175">값</span><span class="sxs-lookup"><span data-stu-id="780db-175">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="780db-176">request-id</span><span class="sxs-lookup"><span data-stu-id="780db-176">request-id</span></span> |<span data-ttu-id="780db-177">String</span><span class="sxs-lookup"><span data-stu-id="780db-177">String</span></span> |<span data-ttu-id="780db-178">현재 작업에 대한 고유 식별자로 서비스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-178">A unique identifier for the current operation, service generated.</span></span> |
| <span data-ttu-id="780db-179">client-request-id</span><span class="sxs-lookup"><span data-stu-id="780db-179">client-request-id</span></span> |<span data-ttu-id="780db-180">String</span><span class="sxs-lookup"><span data-stu-id="780db-180">String</span></span> |<span data-ttu-id="780db-181">호출자가 원래 요청을 통해 지정한 식별자입니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="780db-181">An identifier specified by the caller in the original request, if present.</span></span> |
| <span data-ttu-id="780db-182">Date</span><span class="sxs-lookup"><span data-stu-id="780db-182">Date</span></span> |<span data-ttu-id="780db-183">RFC 1123 날짜</span><span class="sxs-lookup"><span data-stu-id="780db-183">RFC 1123 date</span></span> |<span data-ttu-id="780db-184">요청이 처리된 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-184">The date that the request was processed.</span></span> |
| <span data-ttu-id="780db-185">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="780db-185">Content-Type</span></span> |<span data-ttu-id="780db-186">다름</span><span class="sxs-lookup"><span data-stu-id="780db-186">Varies</span></span> |<span data-ttu-id="780db-187">응답 본문의 콘텐츠 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-187">The content type of the response body.</span></span> |
| <span data-ttu-id="780db-188">Content-Encoding</span><span class="sxs-lookup"><span data-stu-id="780db-188">Content-Encoding</span></span> |<span data-ttu-id="780db-189">다름</span><span class="sxs-lookup"><span data-stu-id="780db-189">Varies</span></span> |<span data-ttu-id="780db-190">Gzip 또는 deflate를 적절하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-190">Gzip or deflate, as appropriate.</span></span> |

## <a name="standard-http-verbs-supported-by-media-services"></a><span data-ttu-id="780db-191">미디어 서비스에서 지원되는 표준 HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="780db-191">Standard HTTP verbs supported by Media Services</span></span>
<span data-ttu-id="780db-192">다음은 HTTP 요청을 만들 때 사용할 수 있는 HTTP 동사의 전체 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="780db-192">The following is a complete list of HTTP verbs that can be used when making HTTP requests:</span></span>

| <span data-ttu-id="780db-193">동사</span><span class="sxs-lookup"><span data-stu-id="780db-193">Verb</span></span> | <span data-ttu-id="780db-194">설명</span><span class="sxs-lookup"><span data-stu-id="780db-194">Description</span></span> |
| --- | --- |
| <span data-ttu-id="780db-195">GET</span><span class="sxs-lookup"><span data-stu-id="780db-195">GET</span></span> |<span data-ttu-id="780db-196">개체의 현재 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-196">Returns the current value of an object.</span></span> |
| <span data-ttu-id="780db-197">POST</span><span class="sxs-lookup"><span data-stu-id="780db-197">POST</span></span> |<span data-ttu-id="780db-198">제공된 데이터를 기반으로 개체를 만들거나 명령을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-198">Creates an object based on the data provided, or submits a command.</span></span> |
| <span data-ttu-id="780db-199">PUT</span><span class="sxs-lookup"><span data-stu-id="780db-199">PUT</span></span> |<span data-ttu-id="780db-200">개체를 바꾸거나 명명된 개체(있는 경우)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="780db-200">Replaces an object, or creates a named object (when applicable).</span></span> |
| <span data-ttu-id="780db-201">삭제</span><span class="sxs-lookup"><span data-stu-id="780db-201">DELETE</span></span> |<span data-ttu-id="780db-202">개체를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-202">Deletes an object.</span></span> |
| <span data-ttu-id="780db-203">MERGE</span><span class="sxs-lookup"><span data-stu-id="780db-203">MERGE</span></span> |<span data-ttu-id="780db-204">명명된 속성 변경 내용으로 기존 개체를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-204">Updates an existing object with named property changes.</span></span> |
| <span data-ttu-id="780db-205">HEAD</span><span class="sxs-lookup"><span data-stu-id="780db-205">HEAD</span></span> |<span data-ttu-id="780db-206">GET 응답에 대한 개체의 메타데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-206">Returns metadata of an object for a GET response.</span></span> |

## <a name="discover-media-services-model"></a><span data-ttu-id="780db-207">Media Services 모델 검색</span><span class="sxs-lookup"><span data-stu-id="780db-207">Discover Media Services model</span></span>
<span data-ttu-id="780db-208">미디어 서비스 엔터티를 더 쉽게 검색할 수 있게 되면 $metadata 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780db-208">To make Media Services entities more discoverable, the $metadata operation can be used.</span></span> <span data-ttu-id="780db-209">유효한 모든 엔터티 형식, 엔터티 속성, 연결, 함수, 동작 등을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="780db-209">It allows you to retrieve all valid entity types, entity properties, associations, functions, actions, and so on.</span></span> <span data-ttu-id="780db-210">다음 예제는 URI https://media.windows.net/API/$metadata를 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="780db-210">The following example shows how to construct the URI: https://media.windows.net/API/$metadata.</span></span>

<span data-ttu-id="780db-211">브라우저에서 메타데이터를 보려면 "? api version=2.x"를 URI의 끝에 추가하거나 귀하의 요청에 x-ms-version 헤더를 포함하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-211">You should append "?api-version=2.x" to the end of the URI if you want to view the metadata in a browser, or do not include the x-ms-version header in your request.</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="780db-212">미디어 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="780db-212">Connect to Media Services</span></span>

<span data-ttu-id="780db-213">AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="780db-213">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="780db-214">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="780db-214">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="780db-215">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="780db-215">You must make subsequent calls to the new URI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="780db-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="780db-216">Next steps</span></span>

<span data-ttu-id="780db-217">REST를 사용하여 AMS API에 액세스하려면 [Azure AD 인증을 사용하여 REST로 Azure Media Services API 액세스](media-services-rest-connect-with-aad.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="780db-217">To access AMS APIs with REST, see [Use Azure AD authentication to access the Azure Media Services API with REST](media-services-rest-connect-with-aad.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="780db-218">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="780db-218">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="780db-219">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="780db-219">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

