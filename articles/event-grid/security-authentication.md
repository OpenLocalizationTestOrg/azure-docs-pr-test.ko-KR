---
title: "aaaAzure 이벤트 표 형태 보안 및 인증"
description: "Azure Event Grid 및 해당 개념을 설명합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="92d5f-103">Event Grid 보안 및 인증</span><span class="sxs-lookup"><span data-stu-id="92d5f-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="92d5f-104">Azure Event Grid에는 세 가지 유형의 인증이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="92d5f-105">이벤트 구독</span><span class="sxs-lookup"><span data-stu-id="92d5f-105">Event subscriptions</span></span>
* <span data-ttu-id="92d5f-106">이벤트 게시</span><span class="sxs-lookup"><span data-stu-id="92d5f-106">Event publishing</span></span>
* <span data-ttu-id="92d5f-107">WebHook 이벤트 전달</span><span class="sxs-lookup"><span data-stu-id="92d5f-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="92d5f-108">WebHook 이벤트 전달</span><span class="sxs-lookup"><span data-stu-id="92d5f-108">WebHook Event delivery</span></span>

<span data-ttu-id="92d5f-109">Webhook이 Azure 이벤트 표 형태에서 실시간으로에서 여러 방법으로 tooreceive 이벤트 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="92d5f-110">새 이벤트 준비 toobe 배달가 있을 때마다 이벤트 표 형태 hello 본문에 tooyour WebHook hello 이벤트와 함께 사용 하는 HTTP 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="92d5f-111">이벤트 표 형태를 사용자 고유의 WebHook 끝점을 등록할 때는 보냅니다 있습니다 간단한 유효성 검사 코드 인 POST 요청은 순서 tooprove 끝점 소유권에.</span><span class="sxs-lookup"><span data-stu-id="92d5f-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="92d5f-112">앱 백 hello 유효성 검사 코드를 출력 하 여 toorespond가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="92d5f-113">이벤트 표 형태 이벤트 hello 유효성 검사에 통과 하지 못한 tooWebHook 끝점 배달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="92d5f-114">유효성 검사 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="92d5f-114">Validation details:</span></span>

* <span data-ttu-id="92d5f-115">이벤트 구독 만들기/업데이트의 hello 시 이벤트 표 형태 "SubscriptionValidationEvent" 이벤트 toohello 대상 끝점을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="92d5f-116">hello 이벤트 "이벤트 형식:: 유효성 검사" 헤더 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="92d5f-117">hello 이벤트 본문 hello에 다른 이벤트 표 형태 이벤트와 동일한 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="92d5f-118">hello 이벤트 데이터 예: 임의로 생성 된 문자열에 "ValidationCode" 속성이 포함 된 “ValidationCode: acb13…”.</span><span class="sxs-lookup"><span data-stu-id="92d5f-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="92d5f-119">순서 tooprove 끝점 소유권 에코 백 hello 유효성 검사 코드 예: "ValidationResponse: acb13...".</span><span class="sxs-lookup"><span data-stu-id="92d5f-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="92d5f-120">마지막으로 Azure 이벤트 표 형태에만 HTTPS webhook 끝점 지원 되는 중요 한 toonote를입니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="92d5f-121">이벤트 구독</span><span class="sxs-lookup"><span data-stu-id="92d5f-121">Event subscription</span></span>

<span data-ttu-id="92d5f-122">toosubscribe tooan 이벤트 있어야 hello **Microsoft.EventGrid/EventSubscriptions/Write** hello에 대 한 권한이 필요한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="92d5f-123">Hello 리소스의 hello 범위에서 새 구독을 작성 하는 때문에이 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="92d5f-124">hello 필요한 리소스 tooa 시스템 항목 또는 사용자 지정 항목은 구독 여부에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="92d5f-125">두 형식은 모두 이 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="92d5f-126">시스템 항목(Azure 서비스 게시자)</span><span class="sxs-lookup"><span data-stu-id="92d5f-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="92d5f-127">시스템 항목에 대 한 사용 권한 toowrite hello 리소스 게시 hello 이벤트의 hello 범위에서 새 이벤트 구독 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="92d5f-128">hello hello 리소스의 형식은 다음과 같습니다.`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="92d5f-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="92d5f-129">라는 저장소 계정에서 예를 들어 toosubscribe tooan 이벤트 **myacct**에 hello Microsoft.EventGrid/EventSubscriptions/Write 권한이 필요 합니다.`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="92d5f-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="92d5f-130">사용자 지정 항목</span><span class="sxs-lookup"><span data-stu-id="92d5f-130">Custom topics</span></span>

<span data-ttu-id="92d5f-131">사용자 지정 항목에 대 한 사용 권한 toowrite hello 이벤트 표 형태 항목의 hello 범위에서 새 이벤트 구독 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="92d5f-132">hello hello 리소스의 형식은 다음과 같습니다.`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="92d5f-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="92d5f-133">예를 들어 toosubscribe tooa 사용자 지정 항목 라는 **mytopic**에 hello Microsoft.EventGrid/EventSubscriptions/Write 권한이 필요 합니다.`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="92d5f-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="92d5f-134">항목 게시</span><span class="sxs-lookup"><span data-stu-id="92d5f-134">Topic publishing</span></span>

<span data-ttu-id="92d5f-135">항목은 SAS(공유 액세스 서명) 또는 키 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="92d5f-136">SAS를 사용하는 것이 좋지만 키 인증에서는 간단한 프로그래밍을 제공하며 기존의 많은 Webhook 게시자와 호환 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="92d5f-137">Hello HTTP 헤더에 hello 인증 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="92d5f-138">SAS를 사용 하 여 **aeg sas 토큰** hello 헤더 값에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="92d5f-139">키 인증을 사용 하 여 **aeg sas 키** hello 헤더 값에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="92d5f-140">키 인증</span><span class="sxs-lookup"><span data-stu-id="92d5f-140">Key authentication</span></span>

<span data-ttu-id="92d5f-141">키 인증은 인증의 hello 가장 간단한 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="92d5f-142">Hello 형식을 사용 합니다.`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="92d5f-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="92d5f-143">예를 들어 다음을 사용하여 키를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="92d5f-144">SAS 토큰</span><span class="sxs-lookup"><span data-stu-id="92d5f-144">SAS tokens</span></span>

<span data-ttu-id="92d5f-145">이벤트 표 형태에 대 한 SAS 토큰에는 hello 리소스, 만료 시간 및 서명을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="92d5f-146">hello hello SAS 토큰 형식이: `r={resource}&e={expiration}&s={signature}`합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="92d5f-147">hello 리소스 경로가 hello 항목 toowhich hello에 대 한 이벤트를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="92d5f-148">예를 들어 올바른 리소스 경로는 다음과 같습니다. `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="92d5f-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="92d5f-149">키에서 hello 서명을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="92d5f-150">예를 들어 유효한 **aeg-sas-token** 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="92d5f-151">다음 예제는 hello 이벤트 표 형태와 사용에 대 한 SAS 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-151">hello following example creates a SAS token for use with Event Grid:</span></span>

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

## <a name="management-access-control"></a><span data-ttu-id="92d5f-152">관리 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="92d5f-152">Management Access Control</span></span>

<span data-ttu-id="92d5f-153">Azure의 이벤트 표 형태 있습니다 toocontrol hello 수준의 허용 지정 된 액세스 toodifferent 사용자 toodo 목록 이벤트 가입 등의 다양 한 관리 작업 하 고 새 데이터베이스를 만들고 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="92d5f-154">Event Grid는 이에 대해 Azure의 RBAC(역할 기반 액세스 확인)를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="92d5f-155">작업 형식</span><span class="sxs-lookup"><span data-stu-id="92d5f-155">Operation types</span></span>

<span data-ttu-id="92d5f-156">Azure 이벤트 표 형태 hello 다음 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="92d5f-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="92d5f-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="92d5f-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="92d5f-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="92d5f-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="92d5f-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="92d5f-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="92d5f-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="92d5f-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="92d5f-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="92d5f-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="92d5f-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="92d5f-163">안녕 마지막 세 작업 반환 잠재적으로 비밀 정보를 일반 읽기 작업에서 필터링을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="92d5f-164">하면 toorestrict 액세스 toothese 작업에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="92d5f-165">사용 하 여 사용자 지정 역할을 만들 수 [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure 명령줄 인터페이스 (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), 및 hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="92d5f-166">RBAC(역할 기반 액세스 확인) 적용</span><span class="sxs-lookup"><span data-stu-id="92d5f-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="92d5f-167">다른 사용자에 대해 단계 tooenforce RBAC를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="92d5f-168">사용자 지정 역할 정의 파일(.json) 만들기</span><span class="sxs-lookup"><span data-stu-id="92d5f-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="92d5f-169">hello 다음은 사용자가 다른 일련의 동작 tooperform 수 있는 샘플 이벤트 표 형태 역할 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="92d5f-170">**EventGridReadOnlyRole.json**: 읽기 전용 작업만을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
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

<span data-ttu-id="92d5f-171">**EventGridNoDeleteListKeysRole.json**: 제한된 게시 작업을 허용하지만 삭제 동작을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
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
 
<span data-ttu-id="92d5f-172">**EventGridContributorRole.json**: 모든 Event Grid 작업을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
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

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="92d5f-173">설치 및 로그인 tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="92d5f-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="92d5f-174">Azure CLI 버전 0.8.8 이상을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="92d5f-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="92d5f-175">Azure 구독으로 참조 tooinstall hello에 대 한 최신 정보 및 연결 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="92d5f-176">Azure CLI에서 Azure Resource Manager입니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="92d5f-177">너무 이동[hello 리소스 관리자를 사용 하 여 hello Azure CLI](../xplat-cli-azure-resource-manager.md) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="92d5f-178">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="92d5f-178">Create a custom role</span></span>

<span data-ttu-id="92d5f-179">사용자 지정 역할 toocreate 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="92d5f-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="92d5f-180">Hello 역할 tooa 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="92d5f-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="92d5f-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="92d5f-181">Next steps</span></span>

* <span data-ttu-id="92d5f-182">소개 tooEvent 표를 참조 하세요. [이벤트 표 형태에 대 한](overview.md)</span><span class="sxs-lookup"><span data-stu-id="92d5f-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
