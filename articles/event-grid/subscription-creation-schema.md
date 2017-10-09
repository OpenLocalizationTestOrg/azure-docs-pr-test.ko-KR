---
title: "aaaAzure 이벤트 표 형태 구독 스키마"
description: "Azure 이벤트 표 형태를 사용 하 여 구독 tooan 이벤트에 대 한 hello 속성을 설명합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="7d13f-103">Event Grid 구독 스키마</span><span class="sxs-lookup"><span data-stu-id="7d13f-103">Event Grid subscription schema</span></span>

<span data-ttu-id="7d13f-104">이벤트 표 형태 구독 toocreate 요청 toohello Create Event subscriptionoperation 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="7d13f-105">형식에 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="7d13f-106">예를 들어 toocreate 라는 저장소 계정에 대 한 이벤트 구독 `examplestorage` 리소스 그룹 이름은 `examplegroup`를 사용 하 여 hello 다음 서식을 지정:</span><span class="sxs-lookup"><span data-stu-id="7d13f-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="7d13f-107">hello 문서 hello 속성 및 hello hello 요청 본문에 대 한 스키마를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="7d13f-108">이벤트 구독 속성</span><span class="sxs-lookup"><span data-stu-id="7d13f-108">Event subscription properties</span></span>

| <span data-ttu-id="7d13f-109">속성</span><span class="sxs-lookup"><span data-stu-id="7d13f-109">Property</span></span> | <span data-ttu-id="7d13f-110">형식</span><span class="sxs-lookup"><span data-stu-id="7d13f-110">Type</span></span> | <span data-ttu-id="7d13f-111">설명</span><span class="sxs-lookup"><span data-stu-id="7d13f-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="7d13f-112">destination</span><span class="sxs-lookup"><span data-stu-id="7d13f-112">destination</span></span> | <span data-ttu-id="7d13f-113">object</span><span class="sxs-lookup"><span data-stu-id="7d13f-113">object</span></span> | <span data-ttu-id="7d13f-114">hello 끝점을 정의 하는 hello 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="7d13f-115">filter</span><span class="sxs-lookup"><span data-stu-id="7d13f-115">filter</span></span> | <span data-ttu-id="7d13f-116">object</span><span class="sxs-lookup"><span data-stu-id="7d13f-116">object</span></span> | <span data-ttu-id="7d13f-117">Hello 유형의 이벤트를 필터링 하기 위한 선택적 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="7d13f-118">대상 개체</span><span class="sxs-lookup"><span data-stu-id="7d13f-118">destination object</span></span>

| <span data-ttu-id="7d13f-119">속성</span><span class="sxs-lookup"><span data-stu-id="7d13f-119">Property</span></span> | <span data-ttu-id="7d13f-120">형식</span><span class="sxs-lookup"><span data-stu-id="7d13f-120">Type</span></span> | <span data-ttu-id="7d13f-121">설명</span><span class="sxs-lookup"><span data-stu-id="7d13f-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="7d13f-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="7d13f-122">endpointType</span></span> | <span data-ttu-id="7d13f-123">string</span><span class="sxs-lookup"><span data-stu-id="7d13f-123">string</span></span> | <span data-ttu-id="7d13f-124">hello 구독 (webhook/HTTP, 이벤트 허브 또는 큐)에 대 한 끝점의 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="7d13f-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="7d13f-125">endpointUrl</span></span> | <span data-ttu-id="7d13f-126">string</span><span class="sxs-lookup"><span data-stu-id="7d13f-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="7d13f-127">필터 개체</span><span class="sxs-lookup"><span data-stu-id="7d13f-127">filter object</span></span>

| <span data-ttu-id="7d13f-128">속성</span><span class="sxs-lookup"><span data-stu-id="7d13f-128">Property</span></span> | <span data-ttu-id="7d13f-129">형식</span><span class="sxs-lookup"><span data-stu-id="7d13f-129">Type</span></span> | <span data-ttu-id="7d13f-130">설명</span><span class="sxs-lookup"><span data-stu-id="7d13f-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="7d13f-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="7d13f-131">includedEventTypes</span></span> | <span data-ttu-id="7d13f-132">array</span><span class="sxs-lookup"><span data-stu-id="7d13f-132">array</span></span> | <span data-ttu-id="7d13f-133">Hello 이벤트 유형을 hello 이벤트 메시지에는 정확히 일치 tooone 이러한 이벤트 유형 이름의 경우에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="7d13f-134">이벤트 이름 hello 이벤트 소스에 대 한 hello 등록 된 이벤트 형식 이름 일치 하지 않는 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="7d13f-135">기본값은 모든 이벤트 유형과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-135">Default matches all event types.</span></span> |
| <span data-ttu-id="7d13f-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="7d13f-136">subjectBeginsWith</span></span> | <span data-ttu-id="7d13f-137">string</span><span class="sxs-lookup"><span data-stu-id="7d13f-137">string</span></span> | <span data-ttu-id="7d13f-138">접두사 일치 필터 toohello 제목 필드 hello 이벤트 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="7d13f-139">빈 문자열 또는 hello 기본 모두와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="7d13f-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="7d13f-140">subjectEndsWith</span></span> | <span data-ttu-id="7d13f-141">string</span><span class="sxs-lookup"><span data-stu-id="7d13f-141">string</span></span> | <span data-ttu-id="7d13f-142">접미사 일치 필터가 toohello 제목 필드 hello 이벤트 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="7d13f-143">빈 문자열 또는 hello 기본 모두와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="7d13f-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="7d13f-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="7d13f-145">string</span><span class="sxs-lookup"><span data-stu-id="7d13f-145">string</span></span> | <span data-ttu-id="7d13f-146">필터에 대한 대/소문자 구분 일치를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="7d13f-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="7d13f-147">예제 구독 스키마</span><span class="sxs-lookup"><span data-stu-id="7d13f-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7d13f-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d13f-148">Next steps</span></span>

* <span data-ttu-id="7d13f-149">소개 tooEvent 표를 참조 하십시오. [이벤트 표 형태는 무엇입니까?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="7d13f-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
