---
title: "Azure Event Grid 보안 및 인증"
description: "Azure Event Grid 및 해당 개념을 설명합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: b6e1c7587c0b47d04862b4850741aaa3b7d191a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="e01e2-103">Event Grid 보안 및 인증</span><span class="sxs-lookup"><span data-stu-id="e01e2-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="e01e2-104">Azure Event Grid에는 세 가지 유형의 인증이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="e01e2-105">이벤트 구독</span><span class="sxs-lookup"><span data-stu-id="e01e2-105">Event subscriptions</span></span>
* <span data-ttu-id="e01e2-106">이벤트 게시</span><span class="sxs-lookup"><span data-stu-id="e01e2-106">Event publishing</span></span>
* <span data-ttu-id="e01e2-107">WebHook 이벤트 전달</span><span class="sxs-lookup"><span data-stu-id="e01e2-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="e01e2-108">WebHook 이벤트 전달</span><span class="sxs-lookup"><span data-stu-id="e01e2-108">WebHook Event delivery</span></span>

<span data-ttu-id="e01e2-109">WebHook은 Azure Event Grid에서 실시간으로 이벤트를 수신하는 여러 가지 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-109">Webhooks are one of many ways to receive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="e01e2-110">새 이벤트가 전송될 준비가 될 때마다 Event Grid는 본문에서 이벤트를 포함한 WebHook에 HTTP 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-110">Every time there is a new event ready to be delivered, Event Grid sends an HTTP request with to your WebHook with the event in the body.</span></span>

<span data-ttu-id="e01e2-111">Event Grid에서 고유한 WebHook 끝점을 등록하는 경우 끝점의 소유권을 증명하기 위해 간단한 유효성 검사 코드를 포함한 POST 요청을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order to prove endpoint ownership.</span></span> <span data-ttu-id="e01e2-112">앱은 유효성 검사 코드를 다시 반환하여 응답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-112">Your app needs to respond by echoing back the validation code.</span></span> <span data-ttu-id="e01e2-113">Event Grid는 유효성 검사에 통과하지 못한 WebHook 끝점에 이벤트를 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-113">Event Grid will not deliver events to WebHook endpoints that have not passed the validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="e01e2-114">유효성 검사 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="e01e2-114">Validation details:</span></span>

* <span data-ttu-id="e01e2-115">이벤트 구독 생성/업데이트 시 Event Grid는 대상 끝점에 "SubscriptionValidationEvent" 이벤트를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-115">At the time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event to the target endpoint.</span></span>
* <span data-ttu-id="e01e2-116">이벤트에는 "이벤트-형식: 유효성 검사" 헤더 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-116">The event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="e01e2-117">이벤트 본문에는 다른 Event Grid 이벤트와 동일한 스키마가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-117">The event body has the same schema as other Event Grid events.</span></span>
* <span data-ttu-id="e01e2-118">이벤트 데이터는 다음과 같이 임의로 생성된 문자열을 포함한 “ValidationCode” 속성을 포함합니다. “ValidationCode: acb13…”.</span><span class="sxs-lookup"><span data-stu-id="e01e2-118">The event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="e01e2-119">끝점 소유권을 증명하기 위해 “ValidationResponse: acb13…”과 같이 유효성 검사 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-119">In order to prove endpoint ownership, echo back the validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="e01e2-120">마지막으로 Azure Event Grid가 HTTPS Webhook 끝점을 지원한다는 점에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-120">Finally, it is important to note that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="e01e2-121">이벤트 구독</span><span class="sxs-lookup"><span data-stu-id="e01e2-121">Event subscription</span></span>

<span data-ttu-id="e01e2-122">이벤트를 구독하려면 필요한 리소스에 대한 **Microsoft.EventGrid/EventSubscriptions/Write** 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-122">To subscribe to an event, you must have the **Microsoft.EventGrid/EventSubscriptions/Write** permission on the required resource.</span></span> <span data-ttu-id="e01e2-123">리소스의 범위에서 새 구독을 작성하기 때문에 이 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-123">You need this permission because you are writing a new subscription at the scope of the resource.</span></span> <span data-ttu-id="e01e2-124">필요한 리소스는 시스템 항목 또는 사용자 지정 항목을 구독하는지 여부에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-124">The required resource differs based on whether you are subscribing to a system topic or custom topic.</span></span> <span data-ttu-id="e01e2-125">두 형식은 모두 이 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="e01e2-126">시스템 항목(Azure 서비스 게시자)</span><span class="sxs-lookup"><span data-stu-id="e01e2-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="e01e2-127">시스템 항목의 경우 이벤트를 게시하는 리소스의 범위에서 새 이벤트 구독을 쓸 수 있는 사용 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-127">For system topics, you need permission to write a new event subscription at the scope of the resource publishing the event.</span></span> <span data-ttu-id="e01e2-128">리소스의 형식은 다음과 같습니다. `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="e01e2-128">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="e01e2-129">예를 들어 **myacct**라는 저장소 계정에 이벤트를 구독하려면 `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`에 대한 Microsoft.EventGrid/EventSubscriptions/Write 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-129">For example, to subscribe to an event on a storage account named **myacct**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="e01e2-130">사용자 지정 항목</span><span class="sxs-lookup"><span data-stu-id="e01e2-130">Custom topics</span></span>

<span data-ttu-id="e01e2-131">사용자 지정 항목의 경우 Event Grid 항목의 범위에서 새 이벤트 구독을 쓸 수 있는 사용 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-131">For custom topics, you need permission to write a new event subscription at the scope of the Event Grid topic.</span></span> <span data-ttu-id="e01e2-132">리소스의 형식은 다음과 같습니다. `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="e01e2-132">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="e01e2-133">예를 들어 **mytopic**이라는 사용자 지정 항목을 구독하려면 `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`에 대한 Microsoft.EventGrid/EventSubscriptions/Write 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-133">For example, to subscribe to a custom topic named **mytopic**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="e01e2-134">항목 게시</span><span class="sxs-lookup"><span data-stu-id="e01e2-134">Topic publishing</span></span>

<span data-ttu-id="e01e2-135">항목은 SAS(공유 액세스 서명) 또는 키 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="e01e2-136">SAS를 사용하는 것이 좋지만 키 인증에서는 간단한 프로그래밍을 제공하며 기존의 많은 Webhook 게시자와 호환 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="e01e2-137">HTTP 헤더에서 인증 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-137">You include the authentication value in the HTTP header.</span></span> <span data-ttu-id="e01e2-138">SAS의 경우 헤더 값에 **aeg-sas-token**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-138">For SAS, use **aeg-sas-token** for the header value.</span></span> <span data-ttu-id="e01e2-139">키 인증의 경우 헤더 값에 **aeg-sas-key**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-139">For key authentication, use **aeg-sas-key** for the header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="e01e2-140">키 인증</span><span class="sxs-lookup"><span data-stu-id="e01e2-140">Key authentication</span></span>

<span data-ttu-id="e01e2-141">키 인증은 인증의 가장 간단한 양식입니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-141">Key authentication is the simplest form of authentication.</span></span> <span data-ttu-id="e01e2-142">사용할 양식은 다음과 같습니다. `aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="e01e2-142">Use the format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="e01e2-143">예를 들어 다음을 사용하여 키를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="e01e2-144">SAS 토큰</span><span class="sxs-lookup"><span data-stu-id="e01e2-144">SAS tokens</span></span>

<span data-ttu-id="e01e2-145">Event Grid의 SAS 토큰에는 리소스, 만료 시간 및 서명이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-145">SAS tokens for Event Grid include the resource, an expiration time, and a signature.</span></span> <span data-ttu-id="e01e2-146">SAS 토큰의 형식은 다음과 같습니다. `r={resource}&e={expiration}&s={signature}`</span><span class="sxs-lookup"><span data-stu-id="e01e2-146">The format of the SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="e01e2-147">리소스는 이벤트를 전송한 항목의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-147">The resource is the path for the topic to which you are sending events.</span></span> <span data-ttu-id="e01e2-148">예를 들어 올바른 리소스 경로는 다음과 같습니다. `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="e01e2-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="e01e2-149">키에서 서명을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-149">You generate the signature from a key.</span></span>

<span data-ttu-id="e01e2-150">예를 들어 유효한 **aeg-sas-token** 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="e01e2-151">다음 예제에서는 Event Grid를 사용하기 위한 SAS 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-151">The following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="e01e2-152">관리 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="e01e2-152">Management Access Control</span></span>

<span data-ttu-id="e01e2-153">Azure Event Grid를 사용하면 여러 사용자가 이벤트 구독 나열, 새 구독 만들기 및 키 생성과 같은 다양한 관리 작업을 수행할 수 있는 액세스 수준을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-153">Azure Event Grid allows you to control the level of access given to different users to do various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="e01e2-154">Event Grid는 이에 대해 Azure의 RBAC(역할 기반 액세스 확인)를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="e01e2-155">작업 형식</span><span class="sxs-lookup"><span data-stu-id="e01e2-155">Operation types</span></span>

<span data-ttu-id="e01e2-156">Azure Event Grid는 다음 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-156">Azure event grid supports the following actions:</span></span>

* <span data-ttu-id="e01e2-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="e01e2-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="e01e2-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="e01e2-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="e01e2-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="e01e2-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="e01e2-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="e01e2-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="e01e2-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="e01e2-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="e01e2-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="e01e2-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="e01e2-163">마지막 세 가지 작업에서는 일반 읽기 작업에서 필터링을 가져오는 비밀 정보를 잠재적으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-163">The last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="e01e2-164">이러한 작업에 대한 액세스를 제한하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-164">It is best practice for you to restrict access to these operations.</span></span> <span data-ttu-id="e01e2-165">[Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure CLI(명령줄 인터페이스)](../active-directory/role-based-access-control-manage-access-azure-cli.md) 및 [REST API](../active-directory/role-based-access-control-manage-access-rest.md)를 사용하여 사용자 지정 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and the [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="e01e2-166">RBAC(역할 기반 액세스 확인) 적용</span><span class="sxs-lookup"><span data-stu-id="e01e2-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="e01e2-167">다음 단계를 사용하여 여러 사용자에게 RBAC를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-167">Use the following steps to enforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="e01e2-168">사용자 지정 역할 정의 파일(.json) 만들기</span><span class="sxs-lookup"><span data-stu-id="e01e2-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="e01e2-169">사용자가 다른 일련의 동작을 수행할 수 있는 샘플 Event Grid 역할 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-169">The following are sample Event Grid role definitions which allow users to perform different sets of actions.</span></span>

<span data-ttu-id="e01e2-170">**EventGridReadOnlyRole.json**: 읽기 전용 작업만을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

<span data-ttu-id="e01e2-171">**EventGridNoDeleteListKeysRole.json**: 제한된 게시 작업을 허용하지만 삭제 동작을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
<span data-ttu-id="e01e2-172">**EventGridContributorRole.json**: 모든 Event Grid 작업을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-to-azure-cli"></a><span data-ttu-id="e01e2-173">Azure CLI에 설치 및 로그인</span><span class="sxs-lookup"><span data-stu-id="e01e2-173">Install and login to Azure CLI</span></span>

* <span data-ttu-id="e01e2-174">Azure CLI 버전 0.8.8 이상을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e01e2-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="e01e2-175">최신 버전을 설치하고 Azure 구독에 연결하려면 [Azure CLI 설치 및 구성 방법](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e01e2-175">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="e01e2-176">Azure CLI에서 Azure Resource Manager입니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="e01e2-177">자세한 내용을 보려면 [리소스 관리자에서 Azure CLI 사용](../xplat-cli-azure-resource-manager.md) 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-177">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="e01e2-178">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="e01e2-178">Create a custom role</span></span>

<span data-ttu-id="e01e2-179">사용자 지정 역할을 만들려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e01e2-179">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-the-role-to-a-user"></a><span data-ttu-id="e01e2-180">사용자에게 역할 할당</span><span class="sxs-lookup"><span data-stu-id="e01e2-180">Assign the role to a user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="e01e2-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e01e2-181">Next steps</span></span>

* <span data-ttu-id="e01e2-182">Event Grid에 대한 소개는 [Event Grid 정보](overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e01e2-182">For an introduction to Event Grid, see [About Event Grid](overview.md)</span></span>
