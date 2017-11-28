---
title: "비동기 작업 aaaAzure | Microsoft Docs"
description: "설명 방법을 tootrack Azure에서 비동기 작업입니다."
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
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="98168-103">Azure 비동기 작업 추적</span><span class="sxs-lookup"><span data-stu-id="98168-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="98168-104">Hello 작업을 신속 하 게 완료할 수 없습니다. 때문에 일부 Azure REST 작업을 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="98168-105">이 항목에서는 값을 비동기 작업의 tootrack hello 상태 hello 응답에서 반환 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="98168-106">비동기 작업의 상태 코드</span><span class="sxs-lookup"><span data-stu-id="98168-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="98168-107">비동기 작업은 처음에 다음 중 하나의 HTTP 상태 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="98168-108">201(만들어짐)</span><span class="sxs-lookup"><span data-stu-id="98168-108">201 (Created)</span></span>
* <span data-ttu-id="98168-109">202(수락됨)</span><span class="sxs-lookup"><span data-stu-id="98168-109">202 (Accepted)</span></span> 

<span data-ttu-id="98168-110">Hello 작업이 성공적으로 완료 되 면 중 하나를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="98168-111">200(확인)</span><span class="sxs-lookup"><span data-stu-id="98168-111">200 (OK)</span></span>
* <span data-ttu-id="98168-112">204(내용 없음)</span><span class="sxs-lookup"><span data-stu-id="98168-112">204 (No Content)</span></span> 

<span data-ttu-id="98168-113">Toohello 참조 [REST API 설명서](/rest/api/) 실행 하는 hello 작업에 대 한 toosee hello 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="98168-114">작업의 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="98168-114">Monitor status of operation</span></span>
<span data-ttu-id="98168-115">hello 비동기 REST 작업 반환 헤더 값을 toodetermine hello 상태를 사용 하 여 hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="98168-116">세 개의 헤더 값 tooexamine는 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98168-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="98168-117">`Azure-AsyncOperation`-Hello hello 작업의 진행 중인 상태 검사에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="98168-118">작업에이 값을 반환 하는 경우 항상 hello 연산의 (위치) 하는 대신 it tootrack hello 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="98168-119">`Location` - 작업이 완료된 시점을 결정하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="98168-120">Azure-AsyncOperation이 반환되지 않은 경우에만 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="98168-121">`Retry-After`-초 toowait 수가 hello 비동기 작업의 hello 상태를 확인 하기 전에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="98168-122">그러나 일부 비동기 작업은 이러한 값을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98168-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="98168-123">예를 들어, 한 번의 작업 및 다른 작업에 대 한 hello 위치 헤더 값에 대 한 tooevaluate hello Azure AsyncOperation 헤더 값을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98168-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="98168-124">요청에 대 한 모든 헤더 값을 검색 하는 대로 hello 헤더 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="98168-125">예를 들어 C#에서는 있습니다 hello 헤더에서 값을 검색 한 `HttpWebResponse` 라는 개체 `response` 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="98168-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="98168-126">Azure-AsyncOperation 요청 및 응답</span><span class="sxs-lookup"><span data-stu-id="98168-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="98168-127">tooget hello 상태 hello 비동기 작업의 Azure AsyncOperation 헤더 값의 GET 요청 toohello URL을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="98168-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="98168-128">이 작업 응답 hello hello 본문이 hello 작업에 대 한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="98168-129">hello 다음 예제는 hello 작업에서 반환 된 hello 가능한 값.</span><span class="sxs-lookup"><span data-stu-id="98168-129">hello following example shows hello possible values returned from hello operation:</span></span>

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

<span data-ttu-id="98168-130">`status`만이 모든 응답에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="98168-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="98168-131">hello 오류 개체가 hello 상태가 실패 또는 취소 됨 일 때 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98168-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="98168-132">다른 모든 값은 선택 사항입니다. 따라서 나타나면 hello 응답 hello 예제 보다 다르게 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98168-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="98168-133">provisioningState 값</span><span class="sxs-lookup"><span data-stu-id="98168-133">provisioningState values</span></span>

<span data-ttu-id="98168-134">리소스 만들기, 업데이트 또는 삭제(PUT, PATCH, DELETE)하는 작업은 일반적으로 `provisioningState` 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="98168-135">작업이 완료되면 다음 세 가지 값 중 하나가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="98168-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="98168-136">성공함</span><span class="sxs-lookup"><span data-stu-id="98168-136">Succeeded</span></span>
* <span data-ttu-id="98168-137">Failed</span><span class="sxs-lookup"><span data-stu-id="98168-137">Failed</span></span>
* <span data-ttu-id="98168-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="98168-138">Canceled</span></span>

<span data-ttu-id="98168-139">다른 모든 값 hello 작업이 계속 실행 되 고 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="98168-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="98168-140">hello 리소스 공급자의 상태를 표시 하는 사용자 지정 된 값을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98168-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="98168-141">예를 들어 나타날 수 있습니다 **"승인 됨"** hello 요청 수신 되어 실행 중인 경우.</span><span class="sxs-lookup"><span data-stu-id="98168-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="98168-142">예제 요청 및 응답</span><span class="sxs-lookup"><span data-stu-id="98168-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="98168-143">가상 컴퓨터 시작(Azure-AsyncOperation에서 202)</span><span class="sxs-lookup"><span data-stu-id="98168-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="98168-144">이 예제에서는 toodetermine의 상태를 hello 하는 방법을 보여 줍니다. **시작** 가상 컴퓨터에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="98168-145">형식에 따라 hello에 hello 초기 요청은입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="98168-146">상태 코드 202를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-146">It returns status code 202.</span></span> <span data-ttu-id="98168-147">Hello 헤더 값에 속하지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98168-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="98168-148">다른 요청 toothat URL을 보내는 hello 비동기 작업의 toocheck hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="98168-149">hello 연산의 hello 상태를 포함 하는 hello 응답 본문:</span><span class="sxs-lookup"><span data-stu-id="98168-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="98168-150">리소스 배포(Azure-AsyncOperation에서 201)</span><span class="sxs-lookup"><span data-stu-id="98168-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="98168-151">이 예제에서는 toodetermine의 상태를 hello 하는 방법을 보여 줍니다. **배포** 리소스 tooAzure를 배포 하기 위한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="98168-152">형식에 따라 hello에 hello 초기 요청은입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="98168-153">상태 코드 201을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-153">It returns status code 201.</span></span> <span data-ttu-id="98168-154">hello hello 응답 본문이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98168-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="98168-155">Hello 헤더 값에 속하지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98168-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="98168-156">다른 요청 toothat URL을 보내는 hello 비동기 작업의 toocheck hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="98168-157">hello 연산의 hello 상태를 포함 하는 hello 응답 본문:</span><span class="sxs-lookup"><span data-stu-id="98168-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="98168-158">Hello 배포 완료 되 면 hello 응답 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98168-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="98168-159">저장소 계정 만들기(위치 및 Retry-After에서 202)</span><span class="sxs-lookup"><span data-stu-id="98168-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="98168-160">이 예제에서는 toodetermine hello의 상태를 hello 하는 방법을 보여 줍니다. **만들** 저장소 계정에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="98168-161">형식에 따라 hello에 hello 초기 요청은입니다.</span><span class="sxs-lookup"><span data-stu-id="98168-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="98168-162">요청 본문 hello hello 저장소 계정에 대 한 속성을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98168-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="98168-163">상태 코드 202를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-163">It returns status code 202.</span></span> <span data-ttu-id="98168-164">Hello 헤더 값에 속하지 hello 다음 두 값에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98168-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="98168-165">개수를 기다린 후 다시 시도 후에 지정 된 시간 (초), 다른 요청 toothat URL을 전송 하 여 hello 비동기 작업의 hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="98168-166">Hello 요청이 실행 되 고, 상태 코드를 202 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="98168-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="98168-167">Hello 요청이 완료 하는 경우 사용자 상태 코드 200, 수신 및 hello hello 응답 본문이 생성 된 hello 저장소 계정의 hello 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98168-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98168-168">Next steps</span></span>

* <span data-ttu-id="98168-169">각 REST 작업에 대한 설명서는 [REST API 설명서](/rest/api/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98168-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="98168-170">Hello 리소스 관리자 REST API를 통해 리소스를 관리 하는 방법에 대 한 정보를 참조 하십시오. [리소스 관리자 REST API를 사용 하 여 hello](resource-manager-rest-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="98168-171">hello 리소스 관리자 REST API를 통해 서식 파일을 배포 하는 방법에 대 한 정보를 참조 하십시오. [리소스 관리자 템플릿 및 리소스 관리자 REST API를 사용 하 여 리소스를 배포](resource-group-template-deploy-rest.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98168-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
