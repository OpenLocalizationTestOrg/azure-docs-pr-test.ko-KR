---
title: "Azure Event Grid 이벤트 스키마"
description: "Azure Event Grid가 있는 이벤트에 제공되는 속성을 설명합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 9e3c7b31ef23b29827d7184dc033227685ed92f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="b4c08-103">Event Grid 이벤트 스키마</span><span class="sxs-lookup"><span data-stu-id="b4c08-103">Event Grid event schema</span></span>

<span data-ttu-id="b4c08-104">이 문서에서는 이벤트에 대한 속성 및 스키마를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-104">This article provides the properties and schema for events.</span></span> <span data-ttu-id="b4c08-105">이벤트는 다섯 개의 필수 문자열 속성 집합과 필수 **데이터** 개체로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="b4c08-106">속성은 모든 게시자에서 모든 이벤트에 공통입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-106">The properties are common to all events from any publisher.</span></span> <span data-ttu-id="b4c08-107">**데이터** 개체는 각 게시자에 특정한 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-107">The **data** object contains properties that are specific to each publisher.</span></span> <span data-ttu-id="b4c08-108">시스템 토픽의 경우 이러한 속성은 Storage 또는 Event Hubs와 같은 리소스 공급자에 특정적입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-108">For system topics, these properties are specific to the resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="b4c08-109">이벤트는 여러 이벤트 개체를 포함할 수 있는 배열의 Azure Event Grid에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-109">Events are sent to Azure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="b4c08-110">단일 이벤트가 하나뿐이면 배열의 길이는 1입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-110">If there is only a single event, the array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="b4c08-111">이벤트 속성</span><span class="sxs-lookup"><span data-stu-id="b4c08-111">Event properties</span></span>

<span data-ttu-id="b4c08-112">모든 이벤트에는 다음과 같은 최상위 수준 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-112">All events will contain the same following top level data.</span></span>

| <span data-ttu-id="b4c08-113">속성</span><span class="sxs-lookup"><span data-stu-id="b4c08-113">Property</span></span> | <span data-ttu-id="b4c08-114">형식</span><span class="sxs-lookup"><span data-stu-id="b4c08-114">Type</span></span> | <span data-ttu-id="b4c08-115">설명</span><span class="sxs-lookup"><span data-stu-id="b4c08-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="b4c08-116">토픽</span><span class="sxs-lookup"><span data-stu-id="b4c08-116">topic</span></span> | <span data-ttu-id="b4c08-117">string</span><span class="sxs-lookup"><span data-stu-id="b4c08-117">string</span></span> | <span data-ttu-id="b4c08-118">이벤트 원본에 대한 전체 리소스 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-118">Full resource path to the event source.</span></span> <span data-ttu-id="b4c08-119">이 필드는 쓸 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-119">This field is not writeable.</span></span> |
| <span data-ttu-id="b4c08-120">subject</span><span class="sxs-lookup"><span data-stu-id="b4c08-120">subject</span></span> | <span data-ttu-id="b4c08-121">string</span><span class="sxs-lookup"><span data-stu-id="b4c08-121">string</span></span> | <span data-ttu-id="b4c08-122">이벤트 주체에 대한 경로가 정의된 게시자입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-122">Publisher defined path to the event subject.</span></span> |
| <span data-ttu-id="b4c08-123">eventType</span><span class="sxs-lookup"><span data-stu-id="b4c08-123">eventType</span></span> | <span data-ttu-id="b4c08-124">string</span><span class="sxs-lookup"><span data-stu-id="b4c08-124">string</span></span> | <span data-ttu-id="b4c08-125">이 이벤트 원본에 대해 등록된 이벤트 유형 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-125">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="b4c08-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="b4c08-126">eventTime</span></span> | <span data-ttu-id="b4c08-127">string</span><span class="sxs-lookup"><span data-stu-id="b4c08-127">string</span></span> | <span data-ttu-id="b4c08-128">공급자의 UTC 시간을 기준으로 이벤트가 생성되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-128">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="b4c08-129">id</span><span class="sxs-lookup"><span data-stu-id="b4c08-129">id</span></span> | <span data-ttu-id="b4c08-130">string</span><span class="sxs-lookup"><span data-stu-id="b4c08-130">string</span></span> | <span data-ttu-id="b4c08-131">이벤트에 대한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-131">Unique identifier for the event.</span></span> |
| <span data-ttu-id="b4c08-132">데이터</span><span class="sxs-lookup"><span data-stu-id="b4c08-132">data</span></span> | <span data-ttu-id="b4c08-133">object</span><span class="sxs-lookup"><span data-stu-id="b4c08-133">object</span></span> | <span data-ttu-id="b4c08-134">특정 리소스 공급자에 대한 이벤트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-134">Event data specific to the resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="b4c08-135">사용할 수 있는 이벤트 원본</span><span class="sxs-lookup"><span data-stu-id="b4c08-135">Available event sources</span></span>

<span data-ttu-id="b4c08-136">다음 이벤트 원본은 Event Grid를 통해 소비에 대한 이벤트를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-136">The following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="b4c08-137">리소스 그룹(관리 작업)</span><span class="sxs-lookup"><span data-stu-id="b4c08-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="b4c08-138">Azure 구독(관리 작업)</span><span class="sxs-lookup"><span data-stu-id="b4c08-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="b4c08-139">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b4c08-139">Event Hubs</span></span>
* <span data-ttu-id="b4c08-140">사용자 지정 토픽</span><span class="sxs-lookup"><span data-stu-id="b4c08-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="b4c08-141">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="b4c08-141">Azure Subscriptions</span></span>

<span data-ttu-id="b4c08-142">Azure 구독에서 이제 VM이 생성되거나 저장소 계정이 삭제될 때와 같이 Azure Resource Manager에서 관리 이벤트를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="b4c08-143">사용할 수 있는 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="b4c08-143">Available event types</span></span>

- <span data-ttu-id="b4c08-144">**Microsoft.Resources.ResourceWriteSuccess**: 리소스 만들기 또는 업데이트 작업이 성공할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="b4c08-145">**Microsoft.Resources.ResourceWriteFailure**: 리소스 만들기 또는 업데이트 작업이 실패할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="b4c08-146">**Microsoft.Resources.ResourceWriteCancel**: 리소스 만들기 또는 업데이트 작업이 취소될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="b4c08-147">**Microsoft.Resources.ResourceDeleteSuccess**: 리소스 삭제 작업이 성공할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="b4c08-148">**Microsoft.Resources.ResourceDeleteFailure**: 리소스 삭제 작업이 실패할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="b4c08-149">**Microsoft.Resources.ResourceDeleteCancel**: 리소스 삭제가 취소될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="b4c08-150">템플릿 배포가 취소되면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="b4c08-151">예제 이벤트 스키마</span><span class="sxs-lookup"><span data-stu-id="b4c08-151">Example event schema</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a><span data-ttu-id="b4c08-152">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="b4c08-152">Resource Groups</span></span>

<span data-ttu-id="b4c08-153">Resource Manager에서 이제 VM이 생성되거나 저장소 계정이 삭제될 때와 같이 Azure Resource Manager에서 관리 이벤트를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="b4c08-154">사용할 수 있는 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="b4c08-154">Available event types</span></span>

- <span data-ttu-id="b4c08-155">**Microsoft.Resources.ResourceWriteSuccess**: 리소스 만들기 또는 업데이트 작업이 성공할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="b4c08-156">**Microsoft.Resources.ResourceWriteFailure**: 리소스 만들기 또는 업데이트 작업이 실패할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="b4c08-157">**Microsoft.Resources.ResourceWriteCancel**: 리소스 만들기 또는 업데이트 작업이 취소될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="b4c08-158">**Microsoft.Resources.ResourceDeleteSuccess**: 리소스 삭제 작업이 성공할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="b4c08-159">**Microsoft.Resources.ResourceDeleteFailure**: 리소스 삭제 작업이 실패할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="b4c08-160">**Microsoft.Resources.ResourceDeleteCancel**: 리소스 삭제가 취소될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="b4c08-161">템플릿 배포가 취소되면 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="b4c08-162">예제 이벤트</span><span class="sxs-lookup"><span data-stu-id="b4c08-162">Example event</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a><span data-ttu-id="b4c08-163">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b4c08-163">Event Hubs</span></span>

<span data-ttu-id="b4c08-164">Event Hubs 이벤트는 현재 파일이 캡처 기능을 사용하여 저장소에 자동으로 전송되는 경우에만 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-164">Event Hubs events are currently only emitted when a file is automatically sent to storage using the Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="b4c08-165">사용할 수 있는 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="b4c08-165">Available event types</span></span>

- <span data-ttu-id="b4c08-166">**Microsoft.EventHub.CaptureFileCreated**: 캡처 파일이 생성될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="b4c08-167">예제 이벤트</span><span class="sxs-lookup"><span data-stu-id="b4c08-167">Example event</span></span>

<span data-ttu-id="b4c08-168">이 샘플 이벤트는 캡처가 파일을 저장하는 경우 발생하는 Event Hubs 이벤트의 스키마를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-168">This sample event shows the schema of an Event Hubs event raised when Capture stores a file.</span></span> 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a><span data-ttu-id="b4c08-169">데이터 이동</span><span class="sxs-lookup"><span data-stu-id="b4c08-169">Azure Blob Storage</span></span>

<span data-ttu-id="b4c08-170">Event Grid와의 통합에 등록한 비공개 미리 보기의 Azure Blob Storage입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="b4c08-171">사용할 수 있는 이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="b4c08-171">Available event types</span></span>

- <span data-ttu-id="b4c08-172">**Microsoft.Storage.BlobCreated**: Blob이 생성될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="b4c08-173">**Microsoft.Storage.BlobDeleted**: Blob이 삭제될 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="b4c08-174">예제 이벤트</span><span class="sxs-lookup"><span data-stu-id="b4c08-174">Example event</span></span>

<span data-ttu-id="b4c08-175">이 샘플 이벤트는 Blob이 생성될 때 발생하는 저장소 이벤트의 스키마를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-175">This sample event shows the schema of a storage event raised when a blob is created.</span></span> 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a><span data-ttu-id="b4c08-176">사용자 지정 토픽</span><span class="sxs-lookup"><span data-stu-id="b4c08-176">Custom Topics</span></span>

<span data-ttu-id="b4c08-177">사용자 지정 이벤트의 데이터 페이로드는 사용자에 의해 정의되고 포맷이 올바른 모든 JSON이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-177">The data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="b4c08-178">최상위 수준 데이터는 표준 리소스 정의 이벤트와 동일한 필드를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-178">The top level data should contain the same fields as standard resource defined events.</span></span> <span data-ttu-id="b4c08-179">사용자 지정 토픽에 이벤트를 게시할 때 라우팅 및 필터링을 지원하도록 이벤트의 주체를 모델링하는 것을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-179">When publishing events to custom topics you should consider modeling the subject of your events to aid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="b4c08-180">예제 이벤트</span><span class="sxs-lookup"><span data-stu-id="b4c08-180">Example event</span></span>

<span data-ttu-id="b4c08-181">다음 예제에서는 사용자 지정 토픽에 대한 이벤트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4c08-181">The following example shows an event for a custom topic:</span></span>
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a><span data-ttu-id="b4c08-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4c08-182">Next steps</span></span>

* <span data-ttu-id="b4c08-183">Event Grid에 대한 소개는 [Event Grid란?](overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c08-183">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="b4c08-184">Event Grid 구독을 만드는 방법을 알아보려면 [Event Grid 구독 스키마](subscription-creation-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c08-184">To learn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
