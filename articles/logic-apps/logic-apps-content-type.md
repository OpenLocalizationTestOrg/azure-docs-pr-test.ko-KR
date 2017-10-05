---
title: "콘텐츠 유형 처리 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps이 디자인 및 런타임 시 콘텐츠 유형을 처리하는 방법"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: ac67838344bbd10384299c086ff096fbe5dec6a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="c7a88-103">논리 앱에서 콘텐츠 유형 처리</span><span class="sxs-lookup"><span data-stu-id="c7a88-103">Handle content types in logic apps</span></span>

<span data-ttu-id="c7a88-104">다양한 유형의 콘텐츠(JSON, XML, 플랫 파일 및 이진 데이터 포함)가 논리 앱을 통해 흐를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="c7a88-105">Logic Apps 엔진이 모든 콘텐츠 유형을 지원하지만 일부는 Logic Apps 엔진에서 고유하게 인식됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-105">While the Logic Apps Engine supports all content types, some are natively understood by the Logic Apps Engine.</span></span> <span data-ttu-id="c7a88-106">필요에 따라 캐스팅 또는 변환이 필요한 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="c7a88-107">이 문서에서는 엔진이 다양한 콘텐츠 유형을 처리하는 방법 및 필요한 경우 이러한 유형을 올바르게 처리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-107">This article describes how the engine handles different content types and how to correctly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="c7a88-108">Content-Type 헤더</span><span class="sxs-lookup"><span data-stu-id="c7a88-108">Content-Type Header</span></span>

<span data-ttu-id="c7a88-109">먼저 논리 앱에서 사용할 수 있는 변환이나 캐스팅이 필요하지 않은 2개의 `Content-Types`인 `application/json` 및 `text/plain`을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-109">To start basically, let's look at the two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="c7a88-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="c7a88-110">Application/JSON</span></span>

<span data-ttu-id="c7a88-111">워크플로 엔진은 HTTP 호출의 `Content-Type` 헤더에 의존하여 적합한 처리를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-111">The workflow engine relies on the `Content-Type` header from HTTP calls to determine the appropriate handling.</span></span> <span data-ttu-id="c7a88-112">콘텐츠 형식 `application/json`을 사용한 요청은 JSON 개체로 저장되고 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-112">Any request with the content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="c7a88-113">또한 JSON 콘텐츠는 기본적으로 캐스팅되지 않고도 구문 분석될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="c7a88-114">예를 들어 이 경우에 `@body('myAction')['foo'][0]`와 같은 식을 사용하여 워크플로에서 콘텐츠 유형 헤더 `application/json `이 있는 요청을 구문 분석하여 `bar` 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-114">For example, you could parse a request that has the content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` to get the value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="c7a88-115">추가 캐스팅은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-115">No additional casting is needed.</span></span> <span data-ttu-id="c7a88-116">JSON 데이터로 작업하지만 헤더를 지정하지 않은 경우 `@json()` 함수(예: `@json(triggerBody())['foo']`)를 사용하여 수동으로 JSON으로 캐스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it to JSON using the `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="c7a88-117">스키마 및 스키마 생성기</span><span class="sxs-lookup"><span data-stu-id="c7a88-117">Schema and schema generator</span></span>

<span data-ttu-id="c7a88-118">요청 트리거를 통해 수신할 것으로 예상되는 페이로드에 대한 JSON 스키마를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-118">The Request trigger lets you to enter a JSON schema for the payload you expect to receive.</span></span> <span data-ttu-id="c7a88-119">이 스키마를 통해 디자이너가 요청의 콘텐츠를 사용할 수 있는 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-119">This schema lets the designer generate tokens so you can consume the content of the request.</span></span> <span data-ttu-id="c7a88-120">준비된 스키마가 없을 경우 샘플 페이로드에서 JSON 스키마를 생성할 수 있도록 **샘플 페이로드를 사용하여 스키마 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-120">If you don't have a schema ready, select **Use sample payload to generate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![스키마](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="c7a88-122">'JSON 구문 분석' 작업</span><span class="sxs-lookup"><span data-stu-id="c7a88-122">'Parse JSON' action</span></span>

<span data-ttu-id="c7a88-123">`Parse JSON` 작업을 통해 논리 앱에 사용하기 위해 친숙한 토큰에 JSON 콘텐츠를 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-123">The `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="c7a88-124">이 작업을 통해 요청 트리거와 마찬가지로 구문 분석하려는 콘텐츠에 맞게 JSON 스키마를 입력하거나 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-124">Similar to the Request trigger, this action lets you enter or generate a JSON schema for the content you want to parse.</span></span> <span data-ttu-id="c7a88-125">이 도구를 통해 Service Bus, Azure Cosmos DB 등의 데이터를 훨씬 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Parse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="c7a88-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="c7a88-127">Text/plain</span></span>

<span data-ttu-id="c7a88-128">`application/json`과 마찬가지로 `text/plain`의 `Content-Type` 헤더와 함께 수신된 HTTP 메시지는 원시 형태로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-128">Similar to `application/json`, HTTP messages received with the `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="c7a88-129">또한 해당 메시지가 캐스팅하지 않고 후속 작업에 포함되는 경우 해당 요청은 `Content-Type`: `text/plain` 헤더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="c7a88-130">예를 들어 플랫 파일을 사용할 경우 `text/plain`과 같은 이 HTTP 콘텐츠가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="c7a88-131">다음 작업에서 요청을 다른 요청의 본문으로 전송한 경우(`@body('flatfile')`) 요청에는 `text/plain` 콘텐츠 유형 헤더가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-131">If in the next action, you send the request as the body of another request (`@body('flatfile')`), the request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="c7a88-132">일반 텍스트 데이터로 작업하지만 헤더를 지정하지 않은 경우 `@string()` 함수(예: `@string(triggerBody())`)를 사용하여 데이터를 수동으로 일반 텍스트로 캐스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast the data to text using the `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="c7a88-133">Application/xml, Application/octet-stream 및 변환기 함수</span><span class="sxs-lookup"><span data-stu-id="c7a88-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="c7a88-134">Logic Apps 엔진은 HTTP 요청 또는 응답에서 수신된 `Content-Type`을 항상 보존합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-134">The Logic Apps Engine always preserves the `Content-Type` that was received on the HTTP request or response.</span></span> <span data-ttu-id="c7a88-135">따라서 엔진에서 `application/octet-stream`의 `Content-Type`을 포함한 컨텐츠를 수신하고 캐스팅 없이 후속 작업에 해당 콘텐츠를 포함하는 경우 보내는 요청에는 `Content-Type`: `application/octet-stream`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-135">So if the engine receives content with the `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, the outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="c7a88-136">이러한 방식으로 엔진은 워크플로를 통해 이동하는 동안 데이터가 손실되지 않도록 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-136">This way, the engine can guarantee data isn't lost while moving through the workflow.</span></span> <span data-ttu-id="c7a88-137">그러나 상태가 워크플로를 통해 이동하면서 작업 상태(입력 및 출력)가 JSON 개체에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-137">However, the action state (inputs and outputs) is stored in a JSON object as the state moves through the workflow.</span></span> <span data-ttu-id="c7a88-138">따라서 일부 데이터 형식을 유지하려면 엔진은 `$content` 및 `$content-type`(자동으로 변환됨) 둘 다를 보존하는 적합한 메타데이터를 사용하여 콘텐츠를 이진 base64 인코딩 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-138">So to preserve some data types, the engine converts the content to a binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="c7a88-139">`@json()` - 데이터를 `application/json`로 캐스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-139">`@json()` - casts data to `application/json`</span></span>
* <span data-ttu-id="c7a88-140">`@xml()` - 데이터를 `application/xml`로 캐스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-140">`@xml()` - casts data to `application/xml`</span></span>
* <span data-ttu-id="c7a88-141">`@binary()` - 데이터를 `application/octet-stream`로 캐스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-141">`@binary()` - casts data to `application/octet-stream`</span></span>
* <span data-ttu-id="c7a88-142">`@string()` - 데이터를 `text/plain`로 캐스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-142">`@string()` - casts data to `text/plain`</span></span>
* <span data-ttu-id="c7a88-143">`@base64()` - 콘텐츠를 base64 문자열로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-143">`@base64()` - converts content to a base64 string</span></span>
* <span data-ttu-id="c7a88-144">`@base64toString()` - base64 인코딩 문자열을 `text/plain`으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-144">`@base64toString()` - converts a base64 encoded string to `text/plain`</span></span>
* <span data-ttu-id="c7a88-145">`@base64toBinary()` - base64 인코딩 문자열을 `application/octet-stream`으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-145">`@base64toBinary()` - converts a base64 encoded string to `application/octet-stream`</span></span>
* <span data-ttu-id="c7a88-146">`@encodeDataUri()` - 문자열을 dataUri 바이트 배열로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="c7a88-147">`@decodeDataUri()` - dataUri를 바이트 배열로 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="c7a88-148">예를 들어 `Content-Type`: `application/xml`인 다음 HTTP 요청을 받은 경우</span><span class="sxs-lookup"><span data-stu-id="c7a88-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="c7a88-149">캐스팅한 후 나중에 `@xml(triggerBody())`라는 항목과 함께 또는 `@xpath(xml(triggerBody()), '/CustomerName')`라는 함수에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="c7a88-150">다른 콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="c7a88-150">Other content types</span></span>

<span data-ttu-id="c7a88-151">다른 콘텐츠 형식이 지원되고 논리 앱에서 작동되지만 `$content`를 디코딩하여 메시지 본문을 수동으로 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-151">Other content types are supported and work with logic apps, but might require manually retrieving the message body by decoding the `$content`.</span></span> <span data-ttu-id="c7a88-152">예를 들어 `$content`가 모든 데이터를 보존하기 위해 base64 문자열로 인코딩된 페이로드인 경우 `application/x-www-url-formencoded` 요청을 트리거한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is the payload encoded as a base64 string to preserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="c7a88-153">요청이 일반 텍스트 또는 JSON이 아니기 때문에 다음과 같이 작업에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-153">Because the request isn't plain text or JSON, the request is stored in the action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

현재 데이터 형식에 대한 네이티브 함수가 없으므로 `@string(body('formdataAction'))`과 같은 함수를 통해 데이터에 수동으로 액세스하여 워크플로에서 이 데이터를 계속 사용할 수 있습니다. 나가는 요청에도 `application/x-www-url-formencoded` 콘텐츠 유형 헤더를 포함하려는 경우 `@body('formdataAction')`과 같이 캐스팅 없이 작업 본문에 요청을 추가할 수 있습니다. 그러나 이 방법은 본문이 `body` 입력의 유일한 매개 변수인 경우에만 작동합니다. <span data-ttu-id="c7a88-157">`application/json` 요청에서 `@body('formdataAction')`을 사용하려는 경우 인코딩된 본문이 전송되기 때문에 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a88-157">If you try to use `@body('formdataAction')` in an `application/json` request, you get a runtime error because the encoded body is sent.</span></span>

