---
title: "Azure Resource Manager 요청 한도 | Microsoft Docs"
description: "구독 한도에 도달할 때 Azure Resource Manager 요청에 제한을 사용하는 방법을 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="f21ba-103">Resource Manager 요청 제한</span><span class="sxs-lookup"><span data-stu-id="f21ba-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="f21ba-104">각 구독 및 테넌트에 대해 Resource Manager는 읽기 요청을 시간당 15,000으로, 쓰기 요청을 시간당 1,200으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="f21ba-105">이러한 한도는 각 Azure Resource Manager 인스턴스에 적용됩니다. 모든 Azure 지역에 여러 인스턴스가 있으며 Azure Resource Manager가 모든 Azure 지역에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="f21ba-106">따라서 사용자 요청이 일반적으로 서로 다른 여러 인스턴스에서 서비스되므로 실제 한도는 위에 나열된 것보다 훨씬 높습니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="f21ba-107">응용 프로그램 또는 스크립트가 이러한 한도에 도달하면 요청을 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="f21ba-108">이 항목에서는 한도에 도달하기 전에 포함하는 나머지 요청을 확인하는 방법과 한도에 도달했을 때 대응하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="f21ba-109">한도에 도달하면 HTTP 상태 코드 **429 너무 많은 요청**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="f21ba-110">요청 수는 구독 또는 테넌트 범위로 한정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="f21ba-111">구독에서 요청을 만드는 동시 응용 프로그램이 여러 개 있는 경우 해당 응용 프로그램의 요청이 함께 추가되어 나머지 요청 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="f21ba-112">구독에 범위가 지정된 요청은 구독에서 리소스 그룹 검색 등과 같은 구독 ID 전달을 포함하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="f21ba-113">테넌트에 범위가 지정된 요청은 올바른 Azure 위치 검색 등과 같은 구독 ID를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="f21ba-114">나머지 요청</span><span class="sxs-lookup"><span data-stu-id="f21ba-114">Remaining requests</span></span>
<span data-ttu-id="f21ba-115">응답 헤더를 검사하여 나머지 요청 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="f21ba-116">각 요청은 나머지 읽기 및 쓰기 요청 수에 대한 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="f21ba-117">다음 표에서는 해당 값을 검사할 수 있는 응답 헤더를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="f21ba-118">응답 헤더</span><span class="sxs-lookup"><span data-stu-id="f21ba-118">Response header</span></span> | <span data-ttu-id="f21ba-119">설명</span><span class="sxs-lookup"><span data-stu-id="f21ba-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f21ba-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="f21ba-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="f21ba-121">구독에 범위가 지정된 나머지 읽기</span><span class="sxs-lookup"><span data-stu-id="f21ba-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="f21ba-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="f21ba-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="f21ba-123">구독에 범위가 지정된 나머지 쓰기</span><span class="sxs-lookup"><span data-stu-id="f21ba-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="f21ba-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="f21ba-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="f21ba-125">테넌트에 범위가 지정된 나머지 읽기</span><span class="sxs-lookup"><span data-stu-id="f21ba-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="f21ba-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="f21ba-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="f21ba-127">테넌트에 범위가 지정된 나머지 쓰기</span><span class="sxs-lookup"><span data-stu-id="f21ba-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="f21ba-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="f21ba-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="f21ba-129">구독에 범위가 지정된 나머지 리소스 종류 요청.</span><span class="sxs-lookup"><span data-stu-id="f21ba-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="f21ba-130">이 헤더 값은 서비스에서 기본 제한을 재정의한 경우에만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="f21ba-131">Resource Manager는 구독 읽기 또는 쓰기 대신 이 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="f21ba-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="f21ba-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="f21ba-133">구독에 범위가 지정된 나머지 리소스 종류 컬렉션 요청.</span><span class="sxs-lookup"><span data-stu-id="f21ba-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="f21ba-134">이 헤더 값은 서비스에서 기본 제한을 재정의한 경우에만 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="f21ba-135">이 값은 나머지 컬렉션 요청 수를 제공합니다(리소스 나열).</span><span class="sxs-lookup"><span data-stu-id="f21ba-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="f21ba-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="f21ba-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="f21ba-137">테넌트에 범위가 지정된 나머지 리소스 종류 요청.</span><span class="sxs-lookup"><span data-stu-id="f21ba-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="f21ba-138">이 헤더는 서비스에서 기본 제한을 재정의한 경우에만 테넌트 수준의 요청에 대해서만 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="f21ba-139">Resource Manager는 테넌트 읽기 또는 쓰기 대신 이 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="f21ba-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="f21ba-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="f21ba-141">테넌트에 범위가 지정된 나머지 리소스 종류 컬렉션 요청.</span><span class="sxs-lookup"><span data-stu-id="f21ba-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="f21ba-142">이 헤더는 서비스에서 기본 제한을 재정의한 경우에만 테넌트 수준의 요청에 대해서만 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="f21ba-143">헤더 값 검색</span><span class="sxs-lookup"><span data-stu-id="f21ba-143">Retrieving the header values</span></span>
<span data-ttu-id="f21ba-144">코드 또는 스크립트에서 이러한 헤더 값을 검색하는 것은 임의의 헤더 값을 검색하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="f21ba-145">예를 들어 **C#**에서는 다음 코드로 **response**로 명명된 **HttpWebResponse** 개체에서 헤더 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="f21ba-146">**PowerShell**에서는 Invoke-WebRequest 작업에서 헤더 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="f21ba-147">또는 디버깅을 위해 나머지 요청을 보려면 **PowerShell** cmdlet에서 **-Debug** 매개 변수를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="f21ba-148">그러면 다음 응답 값을 포함한 많은 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-148">Which returns many values, including the following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="f21ba-149">**Azure CLI**에서 더 많은 자세한 정보 표시 옵션을 사용하여 헤더 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="f21ba-150">그러면 다음 개체를 포함한 많은 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-150">Which returns many values, including the following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="f21ba-151">다음 요청을 보낼 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="f21ba-151">Waiting before sending next request</span></span>
<span data-ttu-id="f21ba-152">요청 제한에 도달하면 Resource Manager는 헤더에서 **429** HTTP 상태 코드 및 **Retry-After** 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="f21ba-153">**Retry-After** 값은 응용 프로그램이 다음 요청을 보낼 때까지 대기(또는 절전)하는 시간(초)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="f21ba-154">재시도 값이 경과하기 전에 요청을 보내면 요청이 처리되지 않고 새 재시도 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f21ba-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f21ba-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f21ba-155">Next steps</span></span>

* <span data-ttu-id="f21ba-156">제한 및 할당량에 대한 자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f21ba-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="f21ba-157">비동기 REST 요청 처리에 대해 알아보려면 [Azure 비동기 작업 추적](resource-manager-async-operations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f21ba-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
