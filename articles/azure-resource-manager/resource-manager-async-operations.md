---
title: "Azure 비동기 작업 | Microsoft Docs"
description: "Azure에서 비동기 작업을 추적하는 방법에 대해 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="5b1b2-103">Azure 비동기 작업 추적</span><span class="sxs-lookup"><span data-stu-id="5b1b2-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="5b1b2-104">작업을 신속하게 완료할 수 없기 때문에 일부 Azure REST 작업을 비동기적으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="5b1b2-105">이 항목에서는 응답에서 반환되는 값을 통해 비동기 작업의 상태를 추적하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="5b1b2-106">비동기 작업의 상태 코드</span><span class="sxs-lookup"><span data-stu-id="5b1b2-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="5b1b2-107">비동기 작업은 처음에 다음 중 하나의 HTTP 상태 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="5b1b2-108">201(만들어짐)</span><span class="sxs-lookup"><span data-stu-id="5b1b2-108">201 (Created)</span></span>
* <span data-ttu-id="5b1b2-109">202(수락됨)</span><span class="sxs-lookup"><span data-stu-id="5b1b2-109">202 (Accepted)</span></span> 

<span data-ttu-id="5b1b2-110">작업이 성공적으로 완료되면 다음 중 하나를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="5b1b2-111">200(확인)</span><span class="sxs-lookup"><span data-stu-id="5b1b2-111">200 (OK)</span></span>
* <span data-ttu-id="5b1b2-112">204(내용 없음)</span><span class="sxs-lookup"><span data-stu-id="5b1b2-112">204 (No Content)</span></span> 

<span data-ttu-id="5b1b2-113">[REST API 설명서](/rest/api/)를 참조하여 실행 중인 작업에 대한 응답을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="5b1b2-114">작업의 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="5b1b2-114">Monitor status of operation</span></span>
<span data-ttu-id="5b1b2-115">비동기 REST 작업은 작업의 상태를 확인하는 데 사용할 수 있는 헤더 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="5b1b2-116">잠재적으로 검사할 세 개의 헤더 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="5b1b2-117">`Azure-AsyncOperation` - 작업의 진행 상태를 확인하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="5b1b2-118">작업이 이 값을 반환하는 경우 위치 대신 작업의 상태를 추적하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="5b1b2-119">`Location` - 작업이 완료된 시점을 결정하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="5b1b2-120">Azure-AsyncOperation이 반환되지 않은 경우에만 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="5b1b2-121">`Retry-After` - 비동기 작업의 상태를 확인하기 전에 대기할 시간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="5b1b2-122">그러나 일부 비동기 작업은 이러한 값을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="5b1b2-123">예를 들어, 한 가지 작업에 대한 Azure-AsyncOperation 헤더 값 및 다른 작업에 대한 위치 헤더 값을 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="5b1b2-124">요청에 대한 모든 헤더 값을 검색하는 경우 헤더 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="5b1b2-125">예를 들어 C#에서는 다음 코드를 사용하여 `response`로 명명된 `HttpWebResponse` 개체에서 헤더 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="5b1b2-126">Azure-AsyncOperation 요청 및 응답</span><span class="sxs-lookup"><span data-stu-id="5b1b2-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="5b1b2-127">비동기 작업의 상태를 가져오려면 Azure-AsyncOperation 헤더 값의 URL에 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="5b1b2-128">이 작업에서 응답의 본문은 작업에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="5b1b2-129">다음 예제에서는 작업에서 반환된 가능한 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-129">The following example shows the possible values returned from the operation:</span></span>

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

<span data-ttu-id="5b1b2-130">`status`만이 모든 응답에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="5b1b2-131">상태가 실패함 또는 취소됨인 경우 오류 개체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="5b1b2-132">다른 값은 모두 선택 사항입니다. 따라서 받은 응답은 예제와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="5b1b2-133">provisioningState 값</span><span class="sxs-lookup"><span data-stu-id="5b1b2-133">provisioningState values</span></span>

<span data-ttu-id="5b1b2-134">리소스 만들기, 업데이트 또는 삭제(PUT, PATCH, DELETE)하는 작업은 일반적으로 `provisioningState` 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="5b1b2-135">작업이 완료되면 다음 세 가지 값 중 하나가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="5b1b2-136">성공함</span><span class="sxs-lookup"><span data-stu-id="5b1b2-136">Succeeded</span></span>
* <span data-ttu-id="5b1b2-137">Failed</span><span class="sxs-lookup"><span data-stu-id="5b1b2-137">Failed</span></span>
* <span data-ttu-id="5b1b2-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="5b1b2-138">Canceled</span></span>

<span data-ttu-id="5b1b2-139">다른 값은 모두 작업이 계속 실행 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="5b1b2-140">리소스 공급자는 해당 상태를 표시하는 사용자 지정된 값을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="5b1b2-141">예를 들어 요청을 받고 실행 중인 경우 **수락됨**을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="5b1b2-142">예제 요청 및 응답</span><span class="sxs-lookup"><span data-stu-id="5b1b2-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="5b1b2-143">가상 컴퓨터 시작(Azure-AsyncOperation에서 202)</span><span class="sxs-lookup"><span data-stu-id="5b1b2-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="5b1b2-144">이 예제에서는 가상 컴퓨터의 **시작** 작업 상태를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="5b1b2-145">초기 요청은 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="5b1b2-146">상태 코드 202를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-146">It returns status code 202.</span></span> <span data-ttu-id="5b1b2-147">헤더 값에서 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="5b1b2-148">비동기 작업의 상태를 확인하려면 다른 요청을 해당 URL로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="5b1b2-149">응답 본문은 작업의 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="5b1b2-150">리소스 배포(Azure-AsyncOperation에서 201)</span><span class="sxs-lookup"><span data-stu-id="5b1b2-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="5b1b2-151">이 예제에서는 Azure에 리소스를 배포하는 **배포** 작업의 상태를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="5b1b2-152">초기 요청은 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="5b1b2-153">상태 코드 201을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-153">It returns status code 201.</span></span> <span data-ttu-id="5b1b2-154">응답의 본문에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="5b1b2-155">헤더 값에서 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="5b1b2-156">비동기 작업의 상태를 확인하려면 다른 요청을 해당 URL로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="5b1b2-157">응답 본문은 작업의 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="5b1b2-158">배포를 마치면 응답에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="5b1b2-159">저장소 계정 만들기(위치 및 Retry-After에서 202)</span><span class="sxs-lookup"><span data-stu-id="5b1b2-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="5b1b2-160">이 예제에서는 저장소 계정의 **만들기** 작업 상태를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="5b1b2-161">초기 요청은 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="5b1b2-162">그리고 요청 본문은 저장소 계정의 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="5b1b2-163">상태 코드 202를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-163">It returns status code 202.</span></span> <span data-ttu-id="5b1b2-164">헤더 값에서 다음 두 개의 값을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="5b1b2-165">Retry-After에서 지정된 시간(초) 동안 대기한 후에 해당 URL에 다른 요청을 전송하여 비동기 작업의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="5b1b2-166">요청을 계속 실행하는 경우 상태 코드 202를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="5b1b2-167">요청이 완료된 경우 사용자는 상태 코드 200를 수신하고 응답의 본문에는 생성된 저장소 계정의 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b1b2-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b1b2-168">Next steps</span></span>

* <span data-ttu-id="5b1b2-169">각 REST 작업에 대한 설명서는 [REST API 설명서](/rest/api/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="5b1b2-170">Resource Manager REST API를 통해 리소스를 관리하는 방법에 대한 정보는 [Resource Manager REST API 사용](resource-manager-rest-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="5b1b2-171">Resource Manager REST API를 통해 템플릿을 배포하는 방법에 대한 정보는 [Resource Manager 템플릿 및 Resource Manager REST API를 사용하여 리소스 배포](resource-group-template-deploy-rest.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b1b2-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>