---
title: "Azure Event Grid 구독 스키마"
description: "Azure Event Grid를 사용하여 이벤트에 대한 구독의 속성을 설명합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: eff2352066a76010d6d882a7b7e1961870cd2d46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="ecbab-103">Event Grid 구독 스키마</span><span class="sxs-lookup"><span data-stu-id="ecbab-103">Event Grid subscription schema</span></span>

<span data-ttu-id="ecbab-104">Event Grid 구독을 만들려면 이벤트 만들기 구독 작업에 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-104">To create an Event Grid subscription, you send a request to the Create Event subscription operation.</span></span> <span data-ttu-id="ecbab-105">이때 다음 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-105">Use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="ecbab-106">예를 들어 `examplegroup`이라는 리소스 그룹의 `examplestorage`라는 저장소 계정에 대한 이벤트 구독을 만들려면 다음 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-106">For example, to create an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="ecbab-107">문서는 요청 본문에 대한 속성 및 스키마를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-107">The article describes the properties and schema for the body of the request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="ecbab-108">이벤트 구독 속성</span><span class="sxs-lookup"><span data-stu-id="ecbab-108">Event subscription properties</span></span>

| <span data-ttu-id="ecbab-109">속성</span><span class="sxs-lookup"><span data-stu-id="ecbab-109">Property</span></span> | <span data-ttu-id="ecbab-110">형식</span><span class="sxs-lookup"><span data-stu-id="ecbab-110">Type</span></span> | <span data-ttu-id="ecbab-111">설명</span><span class="sxs-lookup"><span data-stu-id="ecbab-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="ecbab-112">destination</span><span class="sxs-lookup"><span data-stu-id="ecbab-112">destination</span></span> | <span data-ttu-id="ecbab-113">object</span><span class="sxs-lookup"><span data-stu-id="ecbab-113">object</span></span> | <span data-ttu-id="ecbab-114">끝점을 정의하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-114">The object that defines the endpoint.</span></span> |
| <span data-ttu-id="ecbab-115">filter</span><span class="sxs-lookup"><span data-stu-id="ecbab-115">filter</span></span> | <span data-ttu-id="ecbab-116">object</span><span class="sxs-lookup"><span data-stu-id="ecbab-116">object</span></span> | <span data-ttu-id="ecbab-117">이벤트 유형을 필터링하기 위한 선택적 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-117">An optional field for filtering the types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="ecbab-118">대상 개체</span><span class="sxs-lookup"><span data-stu-id="ecbab-118">destination object</span></span>

| <span data-ttu-id="ecbab-119">속성</span><span class="sxs-lookup"><span data-stu-id="ecbab-119">Property</span></span> | <span data-ttu-id="ecbab-120">형식</span><span class="sxs-lookup"><span data-stu-id="ecbab-120">Type</span></span> | <span data-ttu-id="ecbab-121">설명</span><span class="sxs-lookup"><span data-stu-id="ecbab-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="ecbab-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="ecbab-122">endpointType</span></span> | <span data-ttu-id="ecbab-123">string</span><span class="sxs-lookup"><span data-stu-id="ecbab-123">string</span></span> | <span data-ttu-id="ecbab-124">구독(웹후크/HTTP, Event Hub 또는 큐)에 대한 끝점의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-124">The type of endpoint for the subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="ecbab-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="ecbab-125">endpointUrl</span></span> | <span data-ttu-id="ecbab-126">string</span><span class="sxs-lookup"><span data-stu-id="ecbab-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="ecbab-127">필터 개체</span><span class="sxs-lookup"><span data-stu-id="ecbab-127">filter object</span></span>

| <span data-ttu-id="ecbab-128">속성</span><span class="sxs-lookup"><span data-stu-id="ecbab-128">Property</span></span> | <span data-ttu-id="ecbab-129">형식</span><span class="sxs-lookup"><span data-stu-id="ecbab-129">Type</span></span> | <span data-ttu-id="ecbab-130">설명</span><span class="sxs-lookup"><span data-stu-id="ecbab-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="ecbab-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="ecbab-131">includedEventTypes</span></span> | <span data-ttu-id="ecbab-132">array</span><span class="sxs-lookup"><span data-stu-id="ecbab-132">array</span></span> | <span data-ttu-id="ecbab-133">이벤트 메시지의 이벤트 유형이 이러한 이벤트 유형 이름 중 하나와 정확하게 일치할 때 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-133">Match when the event type in the event message is an exact match to one of these event type names.</span></span> <span data-ttu-id="ecbab-134">이벤트 이름이 이벤트 원본에 대해 등록된 이벤트 유형 이름과 일치하지 않는 경우 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-134">Raises an error when event name does not match the registered event type names for the event source.</span></span> <span data-ttu-id="ecbab-135">기본값은 모든 이벤트 유형과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-135">Default matches all event types.</span></span> |
| <span data-ttu-id="ecbab-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="ecbab-136">subjectBeginsWith</span></span> | <span data-ttu-id="ecbab-137">string</span><span class="sxs-lookup"><span data-stu-id="ecbab-137">string</span></span> | <span data-ttu-id="ecbab-138">이벤트 메시지의 제목 필드에 대한 접두사-일치 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-138">A prefix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="ecbab-139">기본값 또는 빈 문자열은 모두 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-139">The default or empty string matches all.</span></span> | 
| <span data-ttu-id="ecbab-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="ecbab-140">subjectEndsWith</span></span> | <span data-ttu-id="ecbab-141">string</span><span class="sxs-lookup"><span data-stu-id="ecbab-141">string</span></span> | <span data-ttu-id="ecbab-142">이벤트 메시지의 제목 필드에 대한 접미사-일치 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-142">A suffix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="ecbab-143">기본값 또는 빈 문자열은 모두 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-143">The default or empty string matches all.</span></span> |
| <span data-ttu-id="ecbab-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="ecbab-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="ecbab-145">string</span><span class="sxs-lookup"><span data-stu-id="ecbab-145">string</span></span> | <span data-ttu-id="ecbab-146">필터에 대한 대/소문자 구분 일치를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="ecbab-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="ecbab-147">예제 구독 스키마</span><span class="sxs-lookup"><span data-stu-id="ecbab-147">Example subscription schema</span></span>

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="ecbab-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ecbab-148">Next steps</span></span>

* <span data-ttu-id="ecbab-149">Event Grid에 대한 소개는 [Event Grid란?](overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecbab-149">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>