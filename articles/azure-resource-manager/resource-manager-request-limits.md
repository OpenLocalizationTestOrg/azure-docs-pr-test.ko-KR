---
title: "리소스 관리자 요청 제한 aaaAzure | Microsoft Docs"
description: "구독 제한에 도달 하면 Azure 리소스 관리자와 조정 toouse 요청 하는 방식에 대해 설명 합니다."
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
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="5cb6f-103">Resource Manager 요청 제한</span><span class="sxs-lookup"><span data-stu-id="5cb6f-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="5cb6f-104">각 구독 및 테 넌 트에 대 한 리소스 관리자 제한 요청 too15, 000 시간당 읽고 요청 too1, 시간당 200을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="5cb6f-105">이러한 제한이 적용 tooeach Azure 리소스 관리자 인스턴스가; 모든 Azure 지역에서 여러 인스턴스가 있는 및 Azure 리소스 관리자는 배포 된 tooall Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="5cb6f-106">따라서 사용자 요청이 일반적으로 서로 다른 여러 인스턴스에서 서비스되므로 실제 한도는 위에 나열된 것보다 훨씬 높습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="5cb6f-107">응용 프로그램 또는 스크립트는 이러한 한도 도달 해야 toothrottle 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="5cb6f-108">이 항목에서는 남은 toodetermine hello 요청 hello 제한에 도달 하기 전에 보유 하는 방식과 toorespond hello 제한에 도달 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="5cb6f-109">Hello 제한에 도달 하면 hello HTTP 상태 코드 수신 **429 너무 많은 요청**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="5cb6f-110">요청 수가 hello은 범위 지정 된 tooeither 구독 또는 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="5cb6f-111">여러 개 있는 경우 구독에서 요청을 수행 하는 동시 응용 프로그램 hello 요청 해당 응용 프로그램을 함께 추가 됩니다 toodetermine hello 나머지 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="5cb6f-112">범위가 지정 된 구독 요청은 hello 관련 구독에 hello 리소스 그룹을 검색 하는 등를 구독 id를 전달 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="5cb6f-113">테넌트에 범위가 지정된 요청은 올바른 Azure 위치 검색 등과 같은 구독 ID를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="5cb6f-114">나머지 요청</span><span class="sxs-lookup"><span data-stu-id="5cb6f-114">Remaining requests</span></span>
<span data-ttu-id="5cb6f-115">응답 헤더를 검사 하 여 hello 나머지 요청 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="5cb6f-116">각 요청 hello 나머지 읽기 및 쓰기 요청 수에 대 한 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="5cb6f-117">hello 다음 표에서 hello 응답 헤더 값을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="5cb6f-118">응답 헤더</span><span class="sxs-lookup"><span data-stu-id="5cb6f-118">Response header</span></span> | <span data-ttu-id="5cb6f-119">설명</span><span class="sxs-lookup"><span data-stu-id="5cb6f-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5cb6f-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="5cb6f-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="5cb6f-121">구독에 범위가 지정된 나머지 읽기</span><span class="sxs-lookup"><span data-stu-id="5cb6f-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="5cb6f-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="5cb6f-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="5cb6f-123">구독에 범위가 지정된 나머지 쓰기</span><span class="sxs-lookup"><span data-stu-id="5cb6f-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="5cb6f-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="5cb6f-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="5cb6f-125">테넌트에 범위가 지정된 나머지 읽기</span><span class="sxs-lookup"><span data-stu-id="5cb6f-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="5cb6f-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="5cb6f-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="5cb6f-127">테넌트에 범위가 지정된 나머지 쓰기</span><span class="sxs-lookup"><span data-stu-id="5cb6f-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="5cb6f-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="5cb6f-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="5cb6f-129">구독에 범위가 지정된 나머지 리소스 종류 요청.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="5cb6f-130">서비스는 hello 기본 제한을 재정의 한 경우에이 헤더 값이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="5cb6f-131">리소스 관리자는 hello 구독 읽기 또는 쓰기 대신이 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="5cb6f-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="5cb6f-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="5cb6f-133">구독에 범위가 지정된 나머지 리소스 종류 컬렉션 요청.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="5cb6f-134">서비스는 hello 기본 제한을 재정의 한 경우에이 헤더 값이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="5cb6f-135">이 값 hello 다양 한 나머지 컬렉션 요청 (목록 리소스)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="5cb6f-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="5cb6f-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="5cb6f-137">테넌트에 범위가 지정된 나머지 리소스 종류 요청.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="5cb6f-138">테 넌 트 수준에서 요청에 대 한이 헤더에만 추가 됩니다 및 경우 서비스에만 hello 기본 제한을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="5cb6f-139">리소스 관리자는 hello 테 넌 트 읽기 또는 쓰기 대신이 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="5cb6f-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="5cb6f-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="5cb6f-141">테넌트에 범위가 지정된 나머지 리소스 종류 컬렉션 요청.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="5cb6f-142">테 넌 트 수준에서 요청에 대 한이 헤더에만 추가 됩니다 및 경우 서비스에만 hello 기본 제한을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="5cb6f-143">Hello 헤더 값 검색</span><span class="sxs-lookup"><span data-stu-id="5cb6f-143">Retrieving hello header values</span></span>
<span data-ttu-id="5cb6f-144">코드 또는 스크립트에서 이러한 헤더 값을 검색하는 것은 임의의 헤더 값을 검색하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="5cb6f-145">예를 들어 **C#**에서 hello 헤더 값을 검색 한 **HttpWebResponse** 라는 개체 **응답** 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5cb6f-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="5cb6f-146">**PowerShell**을 Invoke-webrequest 작업에서 hello 헤더 값을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="5cb6f-147">하거나, 디버깅에 대 한 요청 toosee hello 남은 hello를 제공할 수 있습니다 사용할 경우 **-디버그** 에 매개 변수 여 **PowerShell** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="5cb6f-148">hello 다음 응답 값을 포함 하 여 여러 개의 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-148">Which returns many values, including hello following response value:</span></span>

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

<span data-ttu-id="5cb6f-149">**Azure CLI**를 사용 하 여 hello 헤더 값을 검색할 hello 더 자세한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="5cb6f-150">hello 다음 개체를 포함 하 여 여러 개의 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-150">Which returns many values, including hello following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="5cb6f-151">다음 요청을 보낼 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="5cb6f-151">Waiting before sending next request</span></span>
<span data-ttu-id="5cb6f-152">리소스 관리자 hello hello 요청 제한에 도달 하는 경우 반환 **429** HTTP 상태 코드와 **Retry-after** hello 헤더의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="5cb6f-153">hello **Retry-after** hello 다음 요청을 보내기 전에 응용 프로그램 대기 해야 하는 시간 (초) (또는 절전 모드) hello 수를 지정 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="5cb6f-154">Hello 다시 시도 값 경과 하기 전에 요청을 보내는 사용자 요청이 처리 되지 않습니다 및 새 다시 시도 값이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cb6f-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cb6f-155">Next steps</span></span>

* <span data-ttu-id="5cb6f-156">제한 및 할당량에 대한 자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="5cb6f-157">비동기 REST 요청을 처리 하는 방법에 대 한 toolearn 참조 [Azure 비동기 작업을 추적](resource-manager-async-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb6f-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
