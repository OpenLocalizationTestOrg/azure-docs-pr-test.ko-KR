---
title: "Azure 논리 앱-aaaHandle 콘텐츠 형식을 | Microsoft Docs"
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
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="b7fce-103">논리 앱에서 콘텐츠 유형 처리</span><span class="sxs-lookup"><span data-stu-id="b7fce-103">Handle content types in logic apps</span></span>

<span data-ttu-id="b7fce-104">다양한 유형의 콘텐츠(JSON, XML, 플랫 파일 및 이진 데이터 포함)가 논리 앱을 통해 흐를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="b7fce-105">논리 앱 엔진 hello 콘텐츠 형식을 모두 지원 하지만, 일부 hello 논리 앱 엔진에서 인식 고유 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="b7fce-106">필요에 따라 캐스팅 또는 변환이 필요한 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="b7fce-107">이 문서에서는 hello 엔진에서 서로 다른 내용 유형을 처리 하는 방법 및 toocorrectly 필요한 경우 이러한 형식을 처리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="b7fce-108">Content-Type 헤더</span><span class="sxs-lookup"><span data-stu-id="b7fce-108">Content-Type Header</span></span>

<span data-ttu-id="b7fce-109">toostart 기본적으로, 살펴보겠습니다 hello 두 `Content-Types` 변환 또는 캐스팅 논리 앱에서 사용할 수 있는 않아도: `application/json` 및 `text/plain`합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="b7fce-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="b7fce-110">Application/JSON</span></span>

<span data-ttu-id="b7fce-111">hello 워크플로 엔진 hello에 의존 `Content-Type` toodetermine hello에 대 한 적절 한 처리를 호출 하는 http에서 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="b7fce-112">모든 요청 hello 콘텐츠 형식과 `application/json` 저장 되 고 JSON 개체로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="b7fce-113">또한 JSON 콘텐츠는 기본적으로 캐스팅되지 않고도 구문 분석될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="b7fce-114">Hello 콘텐츠 형식 헤더가 요청 구문 분석할 수는 예를 들어 `application/json ` 와 같은 식을 사용 하 여 워크플로에서 `@body('myAction')['foo'][0]` tooget hello 값 `bar` 이 경우:</span><span class="sxs-lookup"><span data-stu-id="b7fce-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="b7fce-115">추가 캐스팅은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-115">No additional casting is needed.</span></span> <span data-ttu-id="b7fce-116">JSON 하는데 지정 된 헤더를 포함 하지 않은 데이터로 작업 하는 경우 캐스팅할 수 있습니다 수동으로 hello를 사용 하 여 tooJSON `@json()` 함수 예: `@json(triggerBody())['foo']`합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="b7fce-117">스키마 및 스키마 생성기</span><span class="sxs-lookup"><span data-stu-id="b7fce-117">Schema and schema generator</span></span>

<span data-ttu-id="b7fce-118">hello 요청 트리거 사용 하면 JSON 스키마 tooenter tooreceive hello 페이로드에 대 한 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="b7fce-119">이 스키마는 hello 디자이너를 hello 요청의 hello 콘텐츠를 사용할 수 있도록 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="b7fce-120">준비 되는 스키마를 설정 하지 않은 경우 선택 **사용 샘플 페이로드 toogenerate 스키마**이므로 샘플 페이로드에서 JSON 스키마를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![스키마](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="b7fce-122">'JSON 구문 분석' 작업</span><span class="sxs-lookup"><span data-stu-id="b7fce-122">'Parse JSON' action</span></span>

<span data-ttu-id="b7fce-123">hello `Parse JSON` 동작 논리가 응용 프로그램 사용에 대 한 친숙 한 토큰으로 JSON 콘텐츠를 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="b7fce-124">비슷한 toohello 요청 트리거가 동작을이 수행 하면 입력 하거나 tooparse 원하는 콘텐츠 hello에 대 한 JSON 스키마를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="b7fce-125">이 도구를 통해 Service Bus, Azure Cosmos DB 등의 데이터를 훨씬 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Parse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="b7fce-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="b7fce-127">Text/plain</span></span>

<span data-ttu-id="b7fce-128">비슷한 너무`application/json`, hello 함께 수신 된 HTTP 메시지 `Content-Type` 의 헤더 `text/plain` 원시 형식으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="b7fce-129">또한 해당 메시지가 캐스팅하지 않고 후속 작업에 포함되는 경우 해당 요청은 `Content-Type`: `text/plain` 헤더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="b7fce-130">예를 들어 플랫 파일을 사용할 경우 `text/plain`과 같은 이 HTTP 콘텐츠가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="b7fce-131">Hello 다음 작업을 다른 요청의 hello 본문으로 hello 요청 보내 (`@body('flatfile')`), hello 요청 갖기는 `text/plain` Content-type 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="b7fce-132">데이터는 일반 텍스트 했지만 지정 된 헤더를 사용 하는 경우 수동으로 hello를 사용 하 여 hello 데이터 tootext를 캐스팅할 수 `@string()` 함수 예: `@string(triggerBody())`합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="b7fce-133">Application/xml, Application/octet-stream 및 변환기 함수</span><span class="sxs-lookup"><span data-stu-id="b7fce-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="b7fce-134">논리 앱 엔진 hello hello는 항상 유지 `Content-Type` hello HTTP 요청 또는 응답에 수신 되었다는입니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="b7fce-135">따라서 hello 엔진 hello로 콘텐츠를 받는 경우 `Content-Type` 의 `application/octet-stream`, 캐스팅 하지 않고 후속 작업에서 콘텐츠를 hello 보내는 요청에 포함 `Content-Type`: `application/octet-stream`합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="b7fce-136">이러한 방식으로 hello 엔진 hello 워크플로 통해 이동 하는 동안 데이터가 손실 되지 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="b7fce-137">그러나 hello hello 워크플로 통해 이동 합니다. 상태 대로 (입 / 출력) hello 동작 상태는 JSON 개체에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="b7fce-138">따라서 일부 데이터 형식은 hello 엔진 변환 toopreserve hello 둘 다를 유지 하는 적절 한 메타 데이터와 콘텐츠 tooa 이진 base64 인코딩 문자열 `$content` 및 `$content-type`는 자동으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="b7fce-139">`@json()`-데이터를 너무 캐스팅`application/json`</span><span class="sxs-lookup"><span data-stu-id="b7fce-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="b7fce-140">`@xml()`-데이터를 너무 캐스팅`application/xml`</span><span class="sxs-lookup"><span data-stu-id="b7fce-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="b7fce-141">`@binary()`-데이터를 너무 캐스팅`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="b7fce-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="b7fce-142">`@string()`-데이터를 너무 캐스팅`text/plain`</span><span class="sxs-lookup"><span data-stu-id="b7fce-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="b7fce-143">`@base64()`-콘텐츠 tooa base64 문자열 변환</span><span class="sxs-lookup"><span data-stu-id="b7fce-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="b7fce-144">`@base64toString()`-base64 인코딩 문자열을 너무 변환 합니다.`text/plain`</span><span class="sxs-lookup"><span data-stu-id="b7fce-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="b7fce-145">`@base64toBinary()`-base64 인코딩 문자열을 너무 변환 합니다.`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="b7fce-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="b7fce-146">`@encodeDataUri()` - 문자열을 dataUri 바이트 배열로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="b7fce-147">`@decodeDataUri()` - dataUri를 바이트 배열로 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="b7fce-148">예를 들어 `Content-Type`: `application/xml`인 다음 HTTP 요청을 받은 경우</span><span class="sxs-lookup"><span data-stu-id="b7fce-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="b7fce-149">캐스팅한 후 나중에 `@xml(triggerBody())`라는 항목과 함께 또는 `@xpath(xml(triggerBody()), '/CustomerName')`라는 함수에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="b7fce-150">다른 콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="b7fce-150">Other content types</span></span>

<span data-ttu-id="b7fce-151">다른 콘텐츠 형식을 지원 하 고 논리 앱에서는 작동 하지만 hello 디코딩하여 hello 메시지 본문을 수동으로 검색 하는 동안 필요할 수 있습니다 `$content`합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="b7fce-152">예를 들어, 트리거하는 `application/x-www-url-formencoded` where 요청 `$content` hello 페이로드 데이터가 모두 base64 문자열 toopreserve로 인코딩된:</span><span class="sxs-lookup"><span data-stu-id="b7fce-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="b7fce-153">일반 텍스트 또는 JSON 요청 hello 아니어서 hello 요청이 다음과 같이 hello 동작에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

현재 없는 양식 데이터에 대 한 네이티브 함수, 함수를 사용 하 여 hello 데이터와 같은 이므로 수동으로 액세스 하 여 워크플로에서이 데이터를 여전히 사용할 수 있습니다 있습니다 `@string(body('formdataAction'))`합니다. Hello tooalso hello가 나가는 요청 하려는 경우 `application/x-www-url-formencoded` 콘텐츠 형식 헤더와 같은 캐스팅 없이 hello 요청 toohello 작업 본문을 추가할 수 있습니다 `@body('formdataAction')`합니다. 그러나이 방법을 사용 hello 본문은 hello에서 유일한 매개 변수인 hello `body` 입력 합니다. <span data-ttu-id="b7fce-157">Toouse 하면 `@body('formdataAction')` 에 `application/json` 요청 hello 인코딩된 본문 전송 되기 때문에 런타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7fce-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

