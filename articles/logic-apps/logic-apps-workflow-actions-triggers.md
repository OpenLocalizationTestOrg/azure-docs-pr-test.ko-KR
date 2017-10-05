---
title: "워크플로 작업 및 트리거 - Azure Logic Apps | Microsoft Docs"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="53652-102">Azure Logic Apps의 워크플로 작업 및 트리거</span><span class="sxs-lookup"><span data-stu-id="53652-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="53652-103">논리 앱은 트리거와 작업으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="53652-104">트리거에는 여섯 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-104">There are six types of triggers.</span></span> <span data-ttu-id="53652-105">각 유형마다 서로 다른 인터페이스 및 동작을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="53652-106">[워크플로 정의 언어](logic-apps-workflow-definition-language.md)의 세부 정보를 확인하여 기타 자세한 내용을 알아볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="53652-107">트리거 및 작업에 대한 자세한 내용과 이들을 사용하여 논리 앱을 빌드하고 비즈니스 프로세스 및 워크플로를 개선하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="53652-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="53652-108">트리거</span><span class="sxs-lookup"><span data-stu-id="53652-108">Triggers</span></span>  

<span data-ttu-id="53652-109">트리거는 논리 앱 워크플로의 실행을 시작할 수 있는 호출을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="53652-110">워크플로 실행을 시작하는 두 가지 서로 다른 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-110">Here are the two different ways to initiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="53652-111">폴링 트리거</span><span class="sxs-lookup"><span data-stu-id="53652-111">A polling trigger</span></span>  

-   <span data-ttu-id="53652-112">푸시 트리거 - [워크플로 서비스 REST API](https://docs.microsoft.com/rest/api/logic/workflows) 호출</span><span class="sxs-lookup"><span data-stu-id="53652-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="53652-113">모든 트리거는 다음과 같은 상위 수준 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="53652-114">트리거 유형 및 해당 입력</span><span class="sxs-lookup"><span data-stu-id="53652-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="53652-115">다음과 같은 트리거 유형을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="53652-116">**Request** \- 논리 앱을 사용자가 호출할 끝점으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53652-116">**Request** \- Makes the logic app an endpoint for you to call</span></span>  
  
-   <span data-ttu-id="53652-117">**Recurrence** \- 정의된 일정에 따라 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="53652-118">**HTTP** \- HTTP 웹 끝점을 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="53652-119">HTTP 끝점은 202\-비동기 패턴을 사용하거나 배열을 반환하여 \- 특정 트리거링 계약을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="53652-120">**ApiConnection** \- HTTP 트리거처럼 폴링하지만 [Microsoft 관리 API](https://docs.microsoft.com/azure/connectors/apis-list)를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="53652-121">**HTTPWebhook** \- 수동 트리거처럼 끝점을 열지만 지정된 URL을 호출하여 등록 및 등록 취소도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span></span>  
  
-   <span data-ttu-id="53652-122">**ApiConnectionWebhook** \- Microsoft 관리 API를 활용하여 HTTPWebhook 트리거처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span></span>       
    <span data-ttu-id="53652-123">각 트리거 형식은 해당 동작을 정의하는 서로 다른 **입력** 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="53652-124">요청 트리거</span><span class="sxs-lookup"><span data-stu-id="53652-124">Request trigger</span></span>  

<span data-ttu-id="53652-125">이 트리거는 논리 앱을 호출하는 HTTP 요청을 통해 호출하는 끝점으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span></span> <span data-ttu-id="53652-126">요청 트리거는 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="53652-127">또한 **schema**라는 선택적 속성도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="53652-128">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-128">Element name</span></span>|<span data-ttu-id="53652-129">필수</span><span class="sxs-lookup"><span data-stu-id="53652-129">Required</span></span>|<span data-ttu-id="53652-130">설명</span><span class="sxs-lookup"><span data-stu-id="53652-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="53652-131">schema</span><span class="sxs-lookup"><span data-stu-id="53652-131">schema</span></span>|<span data-ttu-id="53652-132">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-132">No</span></span>|<span data-ttu-id="53652-133">들어오는 요청의 유효성을 검사하는 JSON 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-133">A JSON schema that validates the incoming request.</span></span> <span data-ttu-id="53652-134">후속 워크플로 단계에서 참조할 속성을 파악하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-134">Useful for helping subsequent workflow steps know which properties to reference.</span></span>|

<span data-ttu-id="53652-135">이 끝점을 호출하려면 *listCallbackUrl* API를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span></span> <span data-ttu-id="53652-136">[워크플로 서비스 REST API](https://docs.microsoft.com/rest/api/logic/workflows)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53652-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="53652-137">되풀이 트리거</span><span class="sxs-lookup"><span data-stu-id="53652-137">Recurrence trigger</span></span>  

<span data-ttu-id="53652-138">되풀이 트리거는 정의된 일정에 따라 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="53652-139">이러한 트리거는 다음 예제와 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="53652-140">보시는 바와 같이 워크플로를 실행하는 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-140">As you can see, it is a simple way to run a workflow.</span></span>  
  
|<span data-ttu-id="53652-141">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-141">Element name</span></span>|<span data-ttu-id="53652-142">필수</span><span class="sxs-lookup"><span data-stu-id="53652-142">Required</span></span>|<span data-ttu-id="53652-143">설명</span><span class="sxs-lookup"><span data-stu-id="53652-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="53652-144">frequency</span><span class="sxs-lookup"><span data-stu-id="53652-144">frequency</span></span>|<span data-ttu-id="53652-145">예</span><span class="sxs-lookup"><span data-stu-id="53652-145">Yes</span></span>|<span data-ttu-id="53652-146">트리거가 실행되는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-146">How often the trigger executes.</span></span> <span data-ttu-id="53652-147">second, minute, hour, day, week, month 또는 year 중에 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="53652-148">interval</span><span class="sxs-lookup"><span data-stu-id="53652-148">interval</span></span>|<span data-ttu-id="53652-149">예</span><span class="sxs-lookup"><span data-stu-id="53652-149">Yes</span></span>|<span data-ttu-id="53652-150">되풀이에 대해 지정된 빈도 간격</span><span class="sxs-lookup"><span data-stu-id="53652-150">Interval of the given frequency for the recurrence</span></span>|  
|<span data-ttu-id="53652-151">startTime</span><span class="sxs-lookup"><span data-stu-id="53652-151">startTime</span></span>|<span data-ttu-id="53652-152">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-152">No</span></span>|<span data-ttu-id="53652-153">UTC 오프셋 없이 startTime이 제공될 경우 이 timeZone이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="53652-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="53652-154">timeZone</span></span>|<span data-ttu-id="53652-155">no</span><span class="sxs-lookup"><span data-stu-id="53652-155">no</span></span>|<span data-ttu-id="53652-156">UTC 오프셋 없이 startTime이 제공될 경우 이 timeZone이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="53652-157">미래의 특정 시점에 실행을 시작하도록 트리거를 예약할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-157">You can also schedule a trigger to start executing at some point in the future.</span></span> <span data-ttu-id="53652-158">예를 들어 매주 월요일마다 보고서를 시작하려면 다음 트리거를 만들어 월요일마다 시작하도록 논리 앱을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="53652-159">HTTP 트리거</span><span class="sxs-lookup"><span data-stu-id="53652-159">HTTP trigger</span></span>  

<span data-ttu-id="53652-160">HTTP 트리거는 지정된 끝점을 폴링하고 응답을 확인하여 워크플로를 실행할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span></span> <span data-ttu-id="53652-161">입력 개체는 HTTP 호출을 구성하는 데 필요한 매개 변수 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-161">The inputs object takes the set of parameters required to construct an HTTP call:</span></span>  
  
|<span data-ttu-id="53652-162">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-162">Element name</span></span>|<span data-ttu-id="53652-163">필수</span><span class="sxs-lookup"><span data-stu-id="53652-163">Required</span></span>|<span data-ttu-id="53652-164">설명</span><span class="sxs-lookup"><span data-stu-id="53652-164">Description</span></span>|<span data-ttu-id="53652-165">형식</span><span class="sxs-lookup"><span data-stu-id="53652-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="53652-166">메서드</span><span class="sxs-lookup"><span data-stu-id="53652-166">method</span></span>|<span data-ttu-id="53652-167">yes</span><span class="sxs-lookup"><span data-stu-id="53652-167">yes</span></span>|<span data-ttu-id="53652-168">다음 HTTP 메서드 중 하나일 수 있습니다. GET, POST, PUT, DELETE, PATCH 또는 HEAD</span><span class="sxs-lookup"><span data-stu-id="53652-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="53652-169">문자열</span><span class="sxs-lookup"><span data-stu-id="53652-169">String</span></span>|  
|<span data-ttu-id="53652-170">uri</span><span class="sxs-lookup"><span data-stu-id="53652-170">uri</span></span>|<span data-ttu-id="53652-171">yes</span><span class="sxs-lookup"><span data-stu-id="53652-171">yes</span></span>|<span data-ttu-id="53652-172">호출된 http 또는 https 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-172">The http or https endpoint that is called.</span></span> <span data-ttu-id="53652-173">최대 2킬로바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="53652-174">string</span><span class="sxs-lookup"><span data-stu-id="53652-174">String</span></span>|  
|<span data-ttu-id="53652-175">쿼리</span><span class="sxs-lookup"><span data-stu-id="53652-175">queries</span></span>|<span data-ttu-id="53652-176">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-176">No</span></span>|<span data-ttu-id="53652-177">URL에 추가할 쿼리 매개 변수를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-177">An object representing the query parameters to add to the URL.</span></span> <span data-ttu-id="53652-178">예를 들어 `"queries" : { "api-version": "2015-02-01" }`은 URL에 `?api-version=2015-02-01`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|<span data-ttu-id="53652-179">Object</span><span class="sxs-lookup"><span data-stu-id="53652-179">Object</span></span>|  
|<span data-ttu-id="53652-180">headers</span><span class="sxs-lookup"><span data-stu-id="53652-180">headers</span></span>|<span data-ttu-id="53652-181">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-181">No</span></span>|<span data-ttu-id="53652-182">요청에 전송된 각 헤더를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-182">An object representing each of the headers that is sent to the request.</span></span> <span data-ttu-id="53652-183">예를 들어 요청에 언어 및 형식을 설정하려면 다음과 같이 합니다. `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="53652-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="53652-184">Object</span><span class="sxs-lookup"><span data-stu-id="53652-184">Object</span></span>|  
|<span data-ttu-id="53652-185">body</span><span class="sxs-lookup"><span data-stu-id="53652-185">body</span></span>|<span data-ttu-id="53652-186">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-186">No</span></span>|<span data-ttu-id="53652-187">끝점에 전송된 페이로드를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-187">An object representing the payload that is sent to the endpoint.</span></span>|<span data-ttu-id="53652-188">Object</span><span class="sxs-lookup"><span data-stu-id="53652-188">Object</span></span>|  
|<span data-ttu-id="53652-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="53652-189">retryPolicy</span></span>|<span data-ttu-id="53652-190">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-190">No</span></span>|<span data-ttu-id="53652-191">4xx 또는 5xx 오류에 대한 재시도 동작을 사용자 지정할 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="53652-192">Object</span><span class="sxs-lookup"><span data-stu-id="53652-192">Object</span></span>|  
|<span data-ttu-id="53652-193">authentication</span><span class="sxs-lookup"><span data-stu-id="53652-193">authentication</span></span>|<span data-ttu-id="53652-194">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-194">No</span></span>|<span data-ttu-id="53652-195">요청을 인증해야 하는 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-195">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="53652-196">이 개체에 대한 자세한 내용은 [스케줄러 아웃바운드 인증](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53652-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="53652-197">스케줄러 이외에도 지원되는 속성이 하나 더 있습니다. `authority` 기본적으로 이 값은 지정되지 않은 경우 `https://login.windows.net`이지만 `https://login.windows\-ppe.net`과 같이 다른 대상 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="53652-198">Object</span><span class="sxs-lookup"><span data-stu-id="53652-198">Object</span></span>|  
  
<span data-ttu-id="53652-199">HTTP 트리거가 논리 앱과 잘 작동하도록 하려면 특정 패턴을 따르는 HTTP API가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span></span> <span data-ttu-id="53652-200">다음 필드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-200">It requires the following fields:</span></span>  
  
|<span data-ttu-id="53652-201">응답</span><span class="sxs-lookup"><span data-stu-id="53652-201">Response</span></span>|<span data-ttu-id="53652-202">설명</span><span class="sxs-lookup"><span data-stu-id="53652-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="53652-203">상태 코드</span><span class="sxs-lookup"><span data-stu-id="53652-203">Status code</span></span>|<span data-ttu-id="53652-204">상태 코드 200 \(OK\)이면 실행이 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-204">Status code 200 \(OK\) to cause a run.</span></span> <span data-ttu-id="53652-205">다른 상태 코드이면 실행이 진행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="53652-206">Retry\-after 헤더</span><span class="sxs-lookup"><span data-stu-id="53652-206">Retry\-after header</span></span>|<span data-ttu-id="53652-207">논리 앱이 끝점을 다시 폴링할 때까지 시간(초) 수입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-207">Number of seconds until the logic app polls the endpoint again.</span></span>|  
|<span data-ttu-id="53652-208">위치 헤더</span><span class="sxs-lookup"><span data-stu-id="53652-208">Location header</span></span>|<span data-ttu-id="53652-209">다음 폴링 간격에서 호출할 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-209">The URL to call on the next polling interval.</span></span> <span data-ttu-id="53652-210">지정하지 않으면 원래 URL이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-210">If not specified, the original URL is used.</span></span>|  
  
<span data-ttu-id="53652-211">다양한 요청 유형의 다양한 동작에 대한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="53652-212">응답 코드</span><span class="sxs-lookup"><span data-stu-id="53652-212">Response code</span></span>|<span data-ttu-id="53652-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="53652-213">Retry\-After</span></span>|<span data-ttu-id="53652-214">동작</span><span class="sxs-lookup"><span data-stu-id="53652-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="53652-215">200</span><span class="sxs-lookup"><span data-stu-id="53652-215">200</span></span>|<span data-ttu-id="53652-216">\(없음\)</span><span class="sxs-lookup"><span data-stu-id="53652-216">\(none\)</span></span>|<span data-ttu-id="53652-217">유효한 트리거가 아니므로 Retry\-After가 필요하나, 없는 경우 엔진에서 다음 요청을 폴링하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span></span>|  
|<span data-ttu-id="53652-218">202</span><span class="sxs-lookup"><span data-stu-id="53652-218">202</span></span>|<span data-ttu-id="53652-219">60</span><span class="sxs-lookup"><span data-stu-id="53652-219">60</span></span>|<span data-ttu-id="53652-220">워크플로를 트리거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-220">Do not trigger the workflow.</span></span> <span data-ttu-id="53652-221">1분 후 다음 시도가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-221">The next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="53652-222">200</span><span class="sxs-lookup"><span data-stu-id="53652-222">200</span></span>|<span data-ttu-id="53652-223">10</span><span class="sxs-lookup"><span data-stu-id="53652-223">10</span></span>|<span data-ttu-id="53652-224">워크플로를 실행하고 10초 후 더 많은 내용에 대해 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-224">Run the workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="53652-225">400</span><span class="sxs-lookup"><span data-stu-id="53652-225">400</span></span>|<span data-ttu-id="53652-226">\(없음\)</span><span class="sxs-lookup"><span data-stu-id="53652-226">\(none\)</span></span>|<span data-ttu-id="53652-227">잘못된 요청이며 워크플로를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-227">Bad request, do not run the workflow.</span></span> <span data-ttu-id="53652-228">**다시 시도 정책**이 정의되지 않으면 기본 정책이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-228">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="53652-229">다시 시도 횟수에 도달하면 트리거가 더 이상 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-229">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
|<span data-ttu-id="53652-230">500</span><span class="sxs-lookup"><span data-stu-id="53652-230">500</span></span>|<span data-ttu-id="53652-231">\(없음\)</span><span class="sxs-lookup"><span data-stu-id="53652-231">\(none\)</span></span>|<span data-ttu-id="53652-232">서버 오류이며 워크플로를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-232">Server error, do not run the workflow.</span></span>  <span data-ttu-id="53652-233">**다시 시도 정책**이 정의되지 않으면 기본 정책이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-233">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="53652-234">다시 시도 횟수에 도달하면 트리거가 더 이상 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-234">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="53652-235">HTTP 트리거의 출력은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-235">The outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="53652-236">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-236">Element name</span></span>|<span data-ttu-id="53652-237">설명</span><span class="sxs-lookup"><span data-stu-id="53652-237">Description</span></span>|<span data-ttu-id="53652-238">형식</span><span class="sxs-lookup"><span data-stu-id="53652-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="53652-239">headers</span><span class="sxs-lookup"><span data-stu-id="53652-239">headers</span></span>|<span data-ttu-id="53652-240">http 응답의 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-240">The headers of the http response.</span></span>|<span data-ttu-id="53652-241">Object</span><span class="sxs-lookup"><span data-stu-id="53652-241">Object</span></span>|  
|<span data-ttu-id="53652-242">body</span><span class="sxs-lookup"><span data-stu-id="53652-242">body</span></span>|<span data-ttu-id="53652-243">http 응답의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-243">The body of the http response.</span></span>|<span data-ttu-id="53652-244">Object</span><span class="sxs-lookup"><span data-stu-id="53652-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="53652-245">API 연결 트리거</span><span class="sxs-lookup"><span data-stu-id="53652-245">API Connection trigger</span></span>  

<span data-ttu-id="53652-246">API 연결 트리거는 기본 기능에서 HTTP 트리거와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="53652-247">하지만 작업을 식별하는 매개 변수는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-247">However, the parameters for identifying the action are different.</span></span> <span data-ttu-id="53652-248">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="53652-249">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-249">Element name</span></span>|<span data-ttu-id="53652-250">필수</span><span class="sxs-lookup"><span data-stu-id="53652-250">Required</span></span>|<span data-ttu-id="53652-251">형식</span><span class="sxs-lookup"><span data-stu-id="53652-251">Type</span></span>|<span data-ttu-id="53652-252">설명</span><span class="sxs-lookup"><span data-stu-id="53652-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="53652-253">host</span><span class="sxs-lookup"><span data-stu-id="53652-253">host</span></span>|<span data-ttu-id="53652-254">예</span><span class="sxs-lookup"><span data-stu-id="53652-254">Yes</span></span>||<span data-ttu-id="53652-255">ApiApp 호스트된 게이트웨이 및 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-255">The ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="53652-256">메서드</span><span class="sxs-lookup"><span data-stu-id="53652-256">method</span></span>|<span data-ttu-id="53652-257">예</span><span class="sxs-lookup"><span data-stu-id="53652-257">Yes</span></span>|<span data-ttu-id="53652-258">String</span><span class="sxs-lookup"><span data-stu-id="53652-258">String</span></span>|<span data-ttu-id="53652-259">다음 HTTP 메서드 중 하나일 수 있습니다. **GET**, **POST**, **PUT**, **DELETE**, **PATCH** 또는 **HEAD**</span><span class="sxs-lookup"><span data-stu-id="53652-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="53652-260">쿼리</span><span class="sxs-lookup"><span data-stu-id="53652-260">queries</span></span>|<span data-ttu-id="53652-261">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-261">No</span></span>|<span data-ttu-id="53652-262">Object</span><span class="sxs-lookup"><span data-stu-id="53652-262">Object</span></span>|<span data-ttu-id="53652-263">URL에 추가할 쿼리 매개 변수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-263">Represents the query parameters to be added to the URL.</span></span> <span data-ttu-id="53652-264">예를 들어 `"queries" : { "api-version": "2015-02-01" }`은 URL에 `?api-version=2015-02-01`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="53652-265">headers</span><span class="sxs-lookup"><span data-stu-id="53652-265">headers</span></span>|<span data-ttu-id="53652-266">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-266">No</span></span>|<span data-ttu-id="53652-267">Object</span><span class="sxs-lookup"><span data-stu-id="53652-267">Object</span></span>|<span data-ttu-id="53652-268">요청에 전송된 각 헤더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-268">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="53652-269">예를 들어 요청에 언어 및 형식을 설정하려면 다음과 같이 합니다. `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="53652-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="53652-270">body</span><span class="sxs-lookup"><span data-stu-id="53652-270">body</span></span>|<span data-ttu-id="53652-271">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-271">No</span></span>|<span data-ttu-id="53652-272">Object</span><span class="sxs-lookup"><span data-stu-id="53652-272">Object</span></span>|<span data-ttu-id="53652-273">끝점에 전송된 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-273">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="53652-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="53652-274">retryPolicy</span></span>|<span data-ttu-id="53652-275">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-275">No</span></span>|<span data-ttu-id="53652-276">Object</span><span class="sxs-lookup"><span data-stu-id="53652-276">Object</span></span>|<span data-ttu-id="53652-277">4xx 또는 5xx 오류에 대한 재시도 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="53652-278">authentication</span><span class="sxs-lookup"><span data-stu-id="53652-278">authentication</span></span>|<span data-ttu-id="53652-279">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-279">No</span></span>|<span data-ttu-id="53652-280">Object</span><span class="sxs-lookup"><span data-stu-id="53652-280">Object</span></span>|<span data-ttu-id="53652-281">요청을 인증해야 하는 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-281">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="53652-282">이 개체에 대한 자세한 내용은 [스케줄러 아웃바운드 인증](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53652-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="53652-283">호스트 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-283">The properties for host are:</span></span>  
  
|<span data-ttu-id="53652-284">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-284">Element name</span></span>|<span data-ttu-id="53652-285">필수</span><span class="sxs-lookup"><span data-stu-id="53652-285">Required</span></span>|<span data-ttu-id="53652-286">설명</span><span class="sxs-lookup"><span data-stu-id="53652-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="53652-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="53652-287">api runtimeUrl</span></span>|<span data-ttu-id="53652-288">예</span><span class="sxs-lookup"><span data-stu-id="53652-288">Yes</span></span>|<span data-ttu-id="53652-289">관리 API의 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-289">The endpoint of the managed API.</span></span>|  
|<span data-ttu-id="53652-290">connection name</span><span class="sxs-lookup"><span data-stu-id="53652-290">connection name</span></span>||<span data-ttu-id="53652-291">`$connection`이라는 매개 변수에 대한 참조여야 하며 워크플로에서 사용하는 관리 API 연결의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span></span>|
  
<span data-ttu-id="53652-292">API 연결 트리거의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-292">The outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="53652-293">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-293">Element name</span></span>|<span data-ttu-id="53652-294">형식</span><span class="sxs-lookup"><span data-stu-id="53652-294">Type</span></span>|<span data-ttu-id="53652-295">설명</span><span class="sxs-lookup"><span data-stu-id="53652-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="53652-296">headers</span><span class="sxs-lookup"><span data-stu-id="53652-296">headers</span></span>|<span data-ttu-id="53652-297">Object</span><span class="sxs-lookup"><span data-stu-id="53652-297">Object</span></span>|<span data-ttu-id="53652-298">http 응답의 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-298">The headers of the http response.</span></span>|  
|<span data-ttu-id="53652-299">body</span><span class="sxs-lookup"><span data-stu-id="53652-299">body</span></span>|<span data-ttu-id="53652-300">Object</span><span class="sxs-lookup"><span data-stu-id="53652-300">Object</span></span>|<span data-ttu-id="53652-301">http 응답의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-301">The body of the http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="53652-302">HTTPWebhook 트리거</span><span class="sxs-lookup"><span data-stu-id="53652-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="53652-303">HTTPWebhook 트리거는 수동 트리거처럼 끝점을 열지만 지정된 URL을 호출하여 등록 및 등록 취소도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span></span> <span data-ttu-id="53652-304">HTTPWebhook 트리거의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="53652-305">대부분의 섹션은 선택 사항이며 웹후크의 동작은 어떤 섹션이 제공 또는 생략되었는지에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="53652-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="53652-306">웹후크의 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-306">The properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="53652-307">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-307">Element name</span></span>|<span data-ttu-id="53652-308">필수</span><span class="sxs-lookup"><span data-stu-id="53652-308">Required</span></span>|<span data-ttu-id="53652-309">설명</span><span class="sxs-lookup"><span data-stu-id="53652-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="53652-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="53652-310">subscribe</span></span>|<span data-ttu-id="53652-311">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-311">No</span></span>|<span data-ttu-id="53652-312">트리거가 만들어지고 초기 등록을 수행할 때 호출되는 나가는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span></span>|  
|<span data-ttu-id="53652-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="53652-313">unsubscribe</span></span>|<span data-ttu-id="53652-314">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-314">No</span></span>|<span data-ttu-id="53652-315">트리거가 삭제될 때 나가는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-315">The outgoing request when the trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="53652-316">**Subscribe**은 이벤트 수신 대기를 시작하기 위해 수행되는 나가는 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-316">**Subscribe** is the outgoing call that's made to start listening to events.</span></span> <span data-ttu-id="53652-317">이 호출은 일반 HTTP 작업에서 수행할 때와 동일한 매개 변수 집합으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-317">This call starts with the same set of parameters that the normal HTTP actions do.</span></span> <span data-ttu-id="53652-318">이 나가는 호출은 예를 들어 자격 증명이 롤링되거나 트리거의 입력 매개 변수가 변경될 때마다 등 워크플로가 어떤 식으로든 변경될 때 언제든지 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="53652-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span></span>
  
    <span data-ttu-id="53652-319">이 호출을 지원하기 위해 `@listCallbackUrl()`이라는 새로운 함수가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-319">To support this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="53652-320">이 함수는 이 워크플로에서 특정 트리거에 대해 고유한 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="53652-321">서비스 REST를 사용하는 끝점에 대한 고유한 식별자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-321">It represents the unique identifier for the endpoints that use the Service REST.</span></span>  
  
-   <span data-ttu-id="53652-322">**Unsubscribe**는 다음과 같이 작업에서 이 트리거를 무효화하도록 렌더링할 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="53652-323">트리거 삭제 또는 비활성화</span><span class="sxs-lookup"><span data-stu-id="53652-323">Deleting or disabling the trigger</span></span>  
  
    -   <span data-ttu-id="53652-324">워크플로 삭제 또는 비활성화</span><span class="sxs-lookup"><span data-stu-id="53652-324">Deleting or disabling the workflow</span></span>  
  
    -   <span data-ttu-id="53652-325">구독 삭제 또는 비활성화</span><span class="sxs-lookup"><span data-stu-id="53652-325">Deleting or disabling the subscription</span></span>  
  
    <span data-ttu-id="53652-326">논리 앱에서 구독 취소(unsubscribe) 작업을 자동으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-326">The logic app automatically calls the unsubscribe action.</span></span> <span data-ttu-id="53652-327">이 함수에 대한 매개 변수는 HTTP 트리거와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-327">The parameters to this function are the same as the HTTP trigger.</span></span>  
  
    <span data-ttu-id="53652-328">HTTPWebhook 트리거에 대한 출력은 들어오는 요청의 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span></span>  
  
|<span data-ttu-id="53652-329">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-329">Element name</span></span>|<span data-ttu-id="53652-330">형식</span><span class="sxs-lookup"><span data-stu-id="53652-330">Type</span></span>|<span data-ttu-id="53652-331">설명</span><span class="sxs-lookup"><span data-stu-id="53652-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="53652-332">headers</span><span class="sxs-lookup"><span data-stu-id="53652-332">headers</span></span>|<span data-ttu-id="53652-333">Object</span><span class="sxs-lookup"><span data-stu-id="53652-333">Object</span></span>|<span data-ttu-id="53652-334">http 요청의 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-334">The headers of the http request.</span></span>|  
|<span data-ttu-id="53652-335">body</span><span class="sxs-lookup"><span data-stu-id="53652-335">body</span></span>|<span data-ttu-id="53652-336">Object</span><span class="sxs-lookup"><span data-stu-id="53652-336">Object</span></span>|<span data-ttu-id="53652-337">http 요청의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-337">The body of the http request.</span></span>|  

<span data-ttu-id="53652-338">[HTTP 비동기 제한](#asynchronous-limits)과 동일한 방식으로 웹후크 작업에 대한 제한을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="53652-339">조건</span><span class="sxs-lookup"><span data-stu-id="53652-339">Conditions</span></span>  

<span data-ttu-id="53652-340">모든 트리거에 대해 하나 이상의 조건을 사용하여 워크플로의 실행 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span></span> <span data-ttu-id="53652-341">예:</span><span class="sxs-lookup"><span data-stu-id="53652-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="53652-342">이 경우 워크플로의 `sendReports` 매개 변수가 true로 설정된 동안만 보고서가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span></span> <span data-ttu-id="53652-343">마지막으로 조건에서 트리거의 상태 코드를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-343">Finally, conditions may reference the status code of the trigger.</span></span> <span data-ttu-id="53652-344">예를 들어 다음과 같이 웹 사이트에서 상태 코드 500을 반환하는 경우에만 워크플로를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="53652-345">식에서 트리거의 상태 코드를 참조하는 경우\(어떤 식으로든\) 기본 동작\(200 \(OK\)에서만 트리거됨\)이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="53652-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="53652-346">예를 들어 상태 코드 200 및 상태 코드 201 모두에서 트리거하려면 조건으로 `@or(equals(triggers().code, 200),equals(triggers().code,201))`을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="53652-347">요청에 대해 여러 실행 시작</span><span class="sxs-lookup"><span data-stu-id="53652-347">Start multiple runs for a request</span></span>

<span data-ttu-id="53652-348">단일 요청에 대해 여러 실행을 시작하려면 `splitOn`이 유용합니다. 예를 들어 폴링 간격 중에 새 항목을 여러 개 포함할 수 있는 끝점을 폴링하려는 경우를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="53652-349">`splitOn`에는 트리거 실행을 시작하는 데 각 항목을 사용할 항목 배열을 포함하는 응답 페이로드 내에 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span></span> <span data-ttu-id="53652-350">예를 들어 다음 응답을 반환하는 API가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-350">For example, imagine you have an API that returns the following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="53652-351">논리 앱에는 Rows 콘텐츠만 필요하므로 다음 예제처럼 트리거를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="53652-352">그러면 워크플로 정의에서 `@triggerBody().name`이 첫 번째 실행에 대해 `mycoolrow`를 반환하고 두 번째 실행에 대해 `another row`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span></span> <span data-ttu-id="53652-353">트리거 출력은 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-353">The trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="53652-354">따라서 `SplitOn`을 사용하는 경우 배열 외부의 속성(이 경우 `Status` 필드)을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="53652-355">이 예에서는 `?` 연산자를 사용하여 `Rows` 속성이 없는 경우 오류를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="53652-356">단일 실행 인스턴스</span><span class="sxs-lookup"><span data-stu-id="53652-356">Single run instance</span></span>

<span data-ttu-id="53652-357">모든 활성 실행이 완료된 경우에만 실행할 되풀이 속성이 있는 트리거를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span></span> <span data-ttu-id="53652-358">진행 중인 실행이 있는 동안 예약된 되풀이가 발생하면 트리거는 이를 건너뛰고 다음 예정된 되풀이 간격까지 기다렸다가 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span></span>

<span data-ttu-id="53652-359">작업 옵션을 통해 이 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-359">You can configure this setting through the operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="53652-360">형식 및 입력</span><span class="sxs-lookup"><span data-stu-id="53652-360">Types and inputs</span></span>  

<span data-ttu-id="53652-361">다양한 작업 형식이 있으며 각각 고유한 동작을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="53652-362">컬렉션 작업은 자체적으로 여러 다른 작업을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="53652-363">표준 작업</span><span class="sxs-lookup"><span data-stu-id="53652-363">Standard actions</span></span>  

-   <span data-ttu-id="53652-364">**HTTP** 이 작업은 HTTP 웹 끝점을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="53652-365">**ApiConnection** \- HTTP 작업처럼 동작하지만 Microsoft 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="53652-366">**ApiConnectionWebhook** \- HTTPWebhook와 유사하지만 Microsoft 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="53652-367">**Response** \- 들어오는 호출에 대한 응답을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="53652-368">**Wait** \- 정해진 시간 동안 기다리거나 특정 시간까지 대기하는 단순한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="53652-369">**Workflow** \- 중첩된 워크플로를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="53652-370">**Function** \- 이 작업은 Azure Function을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="53652-371">컬렉션 작업</span><span class="sxs-lookup"><span data-stu-id="53652-371">Collection actions</span></span>

-   <span data-ttu-id="53652-372">**Scope** \- 다른 작업의 논리적 그룹화입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="53652-373">**Condition** \- 식을 평가하고 해당하는 결과 분기를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span></span>

-   <span data-ttu-id="53652-374">**ForEach** \- 이 루프 작업은 배열을 반복하고 각 항목에 대해 내부 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="53652-375">**Until** \- 이 루프 작업은 조건 결과가 true일 때까지 내부 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-375">**Until** \- This looping action executes inner actions until a condition results to true.</span></span>
  
<span data-ttu-id="53652-376">각 작업 형식은 작업의 동작을 정의하는 서로 다른 **입력** 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="53652-377">HTTP 동작</span><span class="sxs-lookup"><span data-stu-id="53652-377">HTTP action</span></span>  

<span data-ttu-id="53652-378">HTTP 작업은 지정된 끝점을 호출하고 응답을 확인하여 워크플로를 실행할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span></span> <span data-ttu-id="53652-379">**입력** 개체는 HTTP 호출을 구성하는 데 필요한 매개 변수 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span></span>  
  
|<span data-ttu-id="53652-380">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-380">Element name</span></span>|<span data-ttu-id="53652-381">필수</span><span class="sxs-lookup"><span data-stu-id="53652-381">Required</span></span>|<span data-ttu-id="53652-382">형식</span><span class="sxs-lookup"><span data-stu-id="53652-382">Type</span></span>|<span data-ttu-id="53652-383">설명</span><span class="sxs-lookup"><span data-stu-id="53652-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="53652-384">메서드</span><span class="sxs-lookup"><span data-stu-id="53652-384">method</span></span>|<span data-ttu-id="53652-385">예</span><span class="sxs-lookup"><span data-stu-id="53652-385">Yes</span></span>|<span data-ttu-id="53652-386">String</span><span class="sxs-lookup"><span data-stu-id="53652-386">String</span></span>|<span data-ttu-id="53652-387">다음 HTTP 메서드 중 하나일 수 있습니다. **GET**, **POST**, **PUT**, **DELETE**, **PATCH** 또는 **HEAD**</span><span class="sxs-lookup"><span data-stu-id="53652-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="53652-388">uri</span><span class="sxs-lookup"><span data-stu-id="53652-388">uri</span></span>|<span data-ttu-id="53652-389">예</span><span class="sxs-lookup"><span data-stu-id="53652-389">Yes</span></span>|<span data-ttu-id="53652-390">String</span><span class="sxs-lookup"><span data-stu-id="53652-390">String</span></span>|<span data-ttu-id="53652-391">호출된 http 또는 https 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-391">The http or https endpoint that is called.</span></span> <span data-ttu-id="53652-392">최대 길이는 2킬로바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="53652-393">쿼리</span><span class="sxs-lookup"><span data-stu-id="53652-393">queries</span></span>|<span data-ttu-id="53652-394">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-394">No</span></span>|<span data-ttu-id="53652-395">Object</span><span class="sxs-lookup"><span data-stu-id="53652-395">Object</span></span>|<span data-ttu-id="53652-396">URL에 추가할 쿼리 매개 변수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-396">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="53652-397">예를 들어 `"queries" : { "api-version": "2015-02-01" }`은 URL에 `?api-version=2015-02-01`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="53652-398">headers</span><span class="sxs-lookup"><span data-stu-id="53652-398">headers</span></span>|<span data-ttu-id="53652-399">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-399">No</span></span>|<span data-ttu-id="53652-400">Object</span><span class="sxs-lookup"><span data-stu-id="53652-400">Object</span></span>|<span data-ttu-id="53652-401">요청에 전송된 각 헤더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-401">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="53652-402">예를 들어 요청에 언어 및 형식을 설정하려면 다음과 같이 합니다. `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="53652-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="53652-403">body</span><span class="sxs-lookup"><span data-stu-id="53652-403">body</span></span>|<span data-ttu-id="53652-404">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-404">No</span></span>|<span data-ttu-id="53652-405">Object</span><span class="sxs-lookup"><span data-stu-id="53652-405">Object</span></span>|<span data-ttu-id="53652-406">끝점에 전송된 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-406">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="53652-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="53652-407">retryPolicy</span></span>|<span data-ttu-id="53652-408">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-408">No</span></span>|<span data-ttu-id="53652-409">Object</span><span class="sxs-lookup"><span data-stu-id="53652-409">Object</span></span>|<span data-ttu-id="53652-410">4xx 또는 5xx 오류에 대한 재시도 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="53652-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="53652-411">operationsOptions</span></span>|<span data-ttu-id="53652-412">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-412">No</span></span>|<span data-ttu-id="53652-413">string</span><span class="sxs-lookup"><span data-stu-id="53652-413">String</span></span>|<span data-ttu-id="53652-414">재정의할 특정 동작 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-414">Defines the set of special behaviors to override.</span></span>|  
|<span data-ttu-id="53652-415">authentication</span><span class="sxs-lookup"><span data-stu-id="53652-415">authentication</span></span>|<span data-ttu-id="53652-416">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-416">No</span></span>|<span data-ttu-id="53652-417">Object</span><span class="sxs-lookup"><span data-stu-id="53652-417">Object</span></span>|<span data-ttu-id="53652-418">요청을 인증해야 하는 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-418">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="53652-419">이 개체에 대한 자세한 내용은 [스케줄러 아웃바운드 인증](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53652-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="53652-420">스케줄러 이외에도 지원되는 속성이 하나 더 있습니다. `authority`</span><span class="sxs-lookup"><span data-stu-id="53652-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="53652-421">기본적으로 지정되지 않은 경우 `https://login.windows.net`이지만 `https://login.windows\-ppe.net`과 같이 다른 대상 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="53652-422">HTTP 작업 \(및 API 연결\) 작업은 다시 시도 정책을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="53652-423">다시 시도 정책은 모든 연결 예외 외에도 HTTP 상태 코드 408, 429 및 5xx로 지정되는 일시적인 오류에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span></span> <span data-ttu-id="53652-424">이 정책은 여기에 표시된 대로 정의된 *retryPolicy* 개체를 사용하여 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-424">This policy is described using the *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="53652-425">재시도 간격은 ISO 8601 형식으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-425">The retry interval is specified in the ISO 8601 format.</span></span> <span data-ttu-id="53652-426">이 간격에는 기본값이 있으며 최소값은 20초인 반면 최대값은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span></span> <span data-ttu-id="53652-427">기본값 및 최대 재시도 횟수는 4시간입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-427">The default and maximum retry count is four hours.</span></span> <span data-ttu-id="53652-428">다시 시도 정책 정의가 지정되지 않은 경우 기본 재시도 횟수 및 간격 값으로 `fixed` 전략이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="53652-429">다시 시도 정책을 사용하지 않도록 설정하려면 해당 형식을 `None`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-429">To disable the retry policy, set its type to `None`.</span></span>  
  
<span data-ttu-id="53652-430">예를 들어 다음 작업은 일시적인 오류가 있는 경우 최신 뉴스 가져오기를 두 번 다시 시도하는 데 각 시도 사이에 30초 지연을 포함하여 총 3번 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="53652-431">비동기 패턴</span><span class="sxs-lookup"><span data-stu-id="53652-431">Asynchronous patterns</span></span>

<span data-ttu-id="53652-432">기본적으로 모든 HTTP 기반 작업은 표준 비동기 작업 패턴을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="53652-433">따라서 원격 서버가 202 \(허용됨\) 응답으로 처리를 위해 요청을 수락했다는 것을 나타내면 Logic Apps 엔진은 터미널 상태가 \(비\-202 응답\)에 도달할 때까지 응답의 위치 헤더에 지정된 URL의 폴링을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="53652-434">이전에 설명된 비동기 동작을 사용하지 않도록 하려면 작업 입력에서 `DisableAsyncPattern` 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span></span> <span data-ttu-id="53652-435">이 경우 작업의 출력은 서버에서 초기 202 응답을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-435">In this case, the output of the action is based on the initial 202 response from the server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="53652-436">비동기 제한</span><span class="sxs-lookup"><span data-stu-id="53652-436">Asynchronous Limits</span></span>

<span data-ttu-id="53652-437">비동기 패턴의 지속 시간은 특정 시간 간격으로 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span></span>  <span data-ttu-id="53652-438">터미널 상태에 도달하지 않고 시간 간격이 경과하면 작업의 상태가 `ActionTimedOut` 코드로 `Cancelled`로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="53652-439">시간 제한은 ISO 8601 형식으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-439">The limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="53652-440">제한은 다음 구문을 사용하여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-440">Limits can be specified with the following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="53652-441">API 연결</span><span class="sxs-lookup"><span data-stu-id="53652-441">API Connection</span></span>  

<span data-ttu-id="53652-442">API 연결은 Microsoft 관리 커넥터를 참조하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="53652-443">이 작업에는 유효한 연결에 대한 참조와 필요한 API 및 매개 변수에 대한 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span></span>

|<span data-ttu-id="53652-444">요소 이름</span><span class="sxs-lookup"><span data-stu-id="53652-444">Element name</span></span>|<span data-ttu-id="53652-445">필수</span><span class="sxs-lookup"><span data-stu-id="53652-445">Required</span></span>|<span data-ttu-id="53652-446">형식</span><span class="sxs-lookup"><span data-stu-id="53652-446">Type</span></span>|<span data-ttu-id="53652-447">설명</span><span class="sxs-lookup"><span data-stu-id="53652-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="53652-448">host</span><span class="sxs-lookup"><span data-stu-id="53652-448">host</span></span>|<span data-ttu-id="53652-449">예</span><span class="sxs-lookup"><span data-stu-id="53652-449">Yes</span></span>|<span data-ttu-id="53652-450">Object</span><span class="sxs-lookup"><span data-stu-id="53652-450">Object</span></span>|<span data-ttu-id="53652-451">runtimeUrl 및 연결 개체에 대한 참조 등 커넥터 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span></span>|
|<span data-ttu-id="53652-452">메서드</span><span class="sxs-lookup"><span data-stu-id="53652-452">method</span></span>|<span data-ttu-id="53652-453">예</span><span class="sxs-lookup"><span data-stu-id="53652-453">Yes</span></span>|<span data-ttu-id="53652-454">String</span><span class="sxs-lookup"><span data-stu-id="53652-454">String</span></span>|<span data-ttu-id="53652-455">다음 HTTP 메서드 중 하나일 수 있습니다. **GET**, **POST**, **PUT**, **DELETE**, **PATCH** 또는 **HEAD**</span><span class="sxs-lookup"><span data-stu-id="53652-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="53652-456">path</span><span class="sxs-lookup"><span data-stu-id="53652-456">path</span></span>|<span data-ttu-id="53652-457">예</span><span class="sxs-lookup"><span data-stu-id="53652-457">Yes</span></span>|<span data-ttu-id="53652-458">문자열</span><span class="sxs-lookup"><span data-stu-id="53652-458">String</span></span>|<span data-ttu-id="53652-459">API 작업의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-459">The path of the API operation.</span></span>|  
|<span data-ttu-id="53652-460">쿼리</span><span class="sxs-lookup"><span data-stu-id="53652-460">queries</span></span>|<span data-ttu-id="53652-461">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-461">No</span></span>|<span data-ttu-id="53652-462">Object</span><span class="sxs-lookup"><span data-stu-id="53652-462">Object</span></span>|<span data-ttu-id="53652-463">URL에 추가할 쿼리 매개 변수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-463">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="53652-464">예를 들어 `"queries" : { "api-version": "2015-02-01" }`은 URL에 `?api-version=2015-02-01`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="53652-465">headers</span><span class="sxs-lookup"><span data-stu-id="53652-465">headers</span></span>|<span data-ttu-id="53652-466">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-466">No</span></span>|<span data-ttu-id="53652-467">Object</span><span class="sxs-lookup"><span data-stu-id="53652-467">Object</span></span>|<span data-ttu-id="53652-468">요청에 전송된 각 헤더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-468">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="53652-469">예를 들어 요청에 언어 및 형식을 설정하려면 다음과 같이 합니다. `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="53652-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="53652-470">body</span><span class="sxs-lookup"><span data-stu-id="53652-470">body</span></span>|<span data-ttu-id="53652-471">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-471">No</span></span>|<span data-ttu-id="53652-472">Object</span><span class="sxs-lookup"><span data-stu-id="53652-472">Object</span></span>|<span data-ttu-id="53652-473">끝점에 전송된 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-473">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="53652-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="53652-474">retryPolicy</span></span>|<span data-ttu-id="53652-475">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-475">No</span></span>|<span data-ttu-id="53652-476">Object</span><span class="sxs-lookup"><span data-stu-id="53652-476">Object</span></span>|<span data-ttu-id="53652-477">4xx 또는 5xx 오류에 대한 재시도 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="53652-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="53652-478">operationsOptions</span></span>|<span data-ttu-id="53652-479">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-479">No</span></span>|<span data-ttu-id="53652-480">string</span><span class="sxs-lookup"><span data-stu-id="53652-480">String</span></span>|<span data-ttu-id="53652-481">재정의할 특정 동작 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-481">Defines the set of special behaviors to override.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="53652-482">API 연결 웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="53652-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="53652-483">[HTTP 비동기 제한](#asynchronous-limits)과 동일한 방식으로 웹후크 작업에 대한 제한을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="53652-484">응답 작업</span><span class="sxs-lookup"><span data-stu-id="53652-484">Response action</span></span>  

<span data-ttu-id="53652-485">이 작업 유형에는 HTTP 요청의 전체 응답 페이로드와 statusCode, body 및 headers가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="53652-486">응답 작업에는 다른 작업에는 적용되지 않는 특수한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-486">The response action has special restrictions that don't apply to other actions.</span></span> <span data-ttu-id="53652-487">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-487">Specifically:</span></span>  
  
-   <span data-ttu-id="53652-488">들어오는 요청에 대해 결정적 응답이 필요하므로 응답 작업은 정의에 병렬일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span></span>  
  
-   <span data-ttu-id="53652-489">들어오는 요청이 응답을 수신한 후 응답 작업에 도달하면 작업은 실패\(충돌\)로 간주되므로 실행은 `Failed`입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span></span>  
  
-   <span data-ttu-id="53652-490">응답 작업이 있는 워크플로는 한 번의 호출로 여러 개의 실행이 발생하므로 해당 트리거에 `splitOn`을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="53652-491">따라서 흐름이 PUT이면 유효성을 검사해야 하며 잘못된 요청이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="53652-492">대기 작업</span><span class="sxs-lookup"><span data-stu-id="53652-492">Wait action</span></span>  

<span data-ttu-id="53652-493">`wait` 작업은 지정된 간격에 워크플로 실행을 일시 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-493">The `wait` action suspends workflow execution for the specified interval.</span></span> <span data-ttu-id="53652-494">예를 들어 15분을 기다리려면 이 코드 조각을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-494">For example, to wait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="53652-495">또는 특정 시점까지 대기하려면 다음 예제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-495">Alternatively, to wait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="53652-496">대기 시간은 **interval** 개체 또는 **until** 개체를 사용하여 지정할 수 있으나 둘 다 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span></span>  
  
|<span data-ttu-id="53652-497">이름</span><span class="sxs-lookup"><span data-stu-id="53652-497">Name</span></span>|<span data-ttu-id="53652-498">필수</span><span class="sxs-lookup"><span data-stu-id="53652-498">Required</span></span>|<span data-ttu-id="53652-499">형식</span><span class="sxs-lookup"><span data-stu-id="53652-499">Type</span></span>|<span data-ttu-id="53652-500">설명</span><span class="sxs-lookup"><span data-stu-id="53652-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="53652-501">interval</span><span class="sxs-lookup"><span data-stu-id="53652-501">interval</span></span>|<span data-ttu-id="53652-502">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-502">No</span></span>|<span data-ttu-id="53652-503">Object</span><span class="sxs-lookup"><span data-stu-id="53652-503">Object</span></span>|<span data-ttu-id="53652-504">시간에 따른 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-504">The wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="53652-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="53652-505">interval unit</span></span>|<span data-ttu-id="53652-506">예</span><span class="sxs-lookup"><span data-stu-id="53652-506">Yes</span></span>|<span data-ttu-id="53652-507">String</span><span class="sxs-lookup"><span data-stu-id="53652-507">String</span></span>|<span data-ttu-id="53652-508">second, minute, hour, day, week, month, year 간격 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="53652-509">interval count</span><span class="sxs-lookup"><span data-stu-id="53652-509">interval count</span></span>|<span data-ttu-id="53652-510">예</span><span class="sxs-lookup"><span data-stu-id="53652-510">Yes</span></span>|<span data-ttu-id="53652-511">String</span><span class="sxs-lookup"><span data-stu-id="53652-511">String</span></span>|<span data-ttu-id="53652-512">지정된 간격 단위에 따른 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-512">Duration based on the given internal unit.</span></span>|  
|<span data-ttu-id="53652-513">until</span><span class="sxs-lookup"><span data-stu-id="53652-513">until</span></span>|<span data-ttu-id="53652-514">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-514">No</span></span>|<span data-ttu-id="53652-515">Object</span><span class="sxs-lookup"><span data-stu-id="53652-515">Object</span></span>|<span data-ttu-id="53652-516">특정 시점에 따른 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-516">The wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="53652-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="53652-517">until timestamp</span></span>|<span data-ttu-id="53652-518">예</span><span class="sxs-lookup"><span data-stu-id="53652-518">Yes</span></span>|<span data-ttu-id="53652-519">String</span><span class="sxs-lookup"><span data-stu-id="53652-519">String</span></span>|<span data-ttu-id="53652-520">String&#124;대기가 만료되는 특정 시점(UTC)입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-520">String&#124;The point in time in UTC when the wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="53652-521">쿼리 작업</span><span class="sxs-lookup"><span data-stu-id="53652-521">Query action</span></span>

<span data-ttu-id="53652-522">`query` 작업을 통해 조건에 따라 배열을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-522">The `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="53652-523">예를 들어 2보다 큰 수를 선택하려면 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-523">For example, to select numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="53652-524">`query` 작업의 출력은 조건을 충족하는 입력 배열의 요소를 포함하는 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span></span>

> [!NOTE]
> <span data-ttu-id="53652-525">`where` 조건을 충족하는 값이 없는 경우 결과는 빈 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-525">If no values satisfy the `where` condition, the result is an empty array.</span></span>

|<span data-ttu-id="53652-526">이름</span><span class="sxs-lookup"><span data-stu-id="53652-526">Name</span></span>|<span data-ttu-id="53652-527">필수</span><span class="sxs-lookup"><span data-stu-id="53652-527">Required</span></span>|<span data-ttu-id="53652-528">형식</span><span class="sxs-lookup"><span data-stu-id="53652-528">Type</span></span>|<span data-ttu-id="53652-529">설명</span><span class="sxs-lookup"><span data-stu-id="53652-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="53652-530">from</span><span class="sxs-lookup"><span data-stu-id="53652-530">from</span></span>|<span data-ttu-id="53652-531">예</span><span class="sxs-lookup"><span data-stu-id="53652-531">Yes</span></span>|<span data-ttu-id="53652-532">배열</span><span class="sxs-lookup"><span data-stu-id="53652-532">Array</span></span>|<span data-ttu-id="53652-533">원본 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-533">The source array.</span></span>|
|<span data-ttu-id="53652-534">여기서,</span><span class="sxs-lookup"><span data-stu-id="53652-534">where</span></span>|<span data-ttu-id="53652-535">예</span><span class="sxs-lookup"><span data-stu-id="53652-535">Yes</span></span>|<span data-ttu-id="53652-536">String</span><span class="sxs-lookup"><span data-stu-id="53652-536">String</span></span>|<span data-ttu-id="53652-537">원본 배열의 각 요소에 적용할 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-537">The condition to apply to each element of the source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="53652-538">작업 선택</span><span class="sxs-lookup"><span data-stu-id="53652-538">Select action</span></span>

<span data-ttu-id="53652-539">`select` 작업은 배열의 각 요소를 새 값으로 프로젝션하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-539">The `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="53652-540">예를 들어 숫자 배열을 개체 배열로 변환하려면 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-540">For example, to convert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="53652-541">`select` 작업의 출력은 `select` 속성으로 정의되어 변환된 입력 배열과 동일한 카디널리티를 가진 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span></span> <span data-ttu-id="53652-542">입력이 빈 배열인 경우 출력도 빈 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-542">If the input is an empty array, the output is also an empty array.</span></span>

|<span data-ttu-id="53652-543">이름</span><span class="sxs-lookup"><span data-stu-id="53652-543">Name</span></span>|<span data-ttu-id="53652-544">필수</span><span class="sxs-lookup"><span data-stu-id="53652-544">Required</span></span>|<span data-ttu-id="53652-545">형식</span><span class="sxs-lookup"><span data-stu-id="53652-545">Type</span></span>|<span data-ttu-id="53652-546">설명</span><span class="sxs-lookup"><span data-stu-id="53652-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="53652-547">from</span><span class="sxs-lookup"><span data-stu-id="53652-547">from</span></span>|<span data-ttu-id="53652-548">예</span><span class="sxs-lookup"><span data-stu-id="53652-548">Yes</span></span>|<span data-ttu-id="53652-549">배열</span><span class="sxs-lookup"><span data-stu-id="53652-549">Array</span></span>|<span data-ttu-id="53652-550">원본 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-550">The source array.</span></span>|
|<span data-ttu-id="53652-551">선택</span><span class="sxs-lookup"><span data-stu-id="53652-551">select</span></span>|<span data-ttu-id="53652-552">예</span><span class="sxs-lookup"><span data-stu-id="53652-552">Yes</span></span>|<span data-ttu-id="53652-553">모두</span><span class="sxs-lookup"><span data-stu-id="53652-553">Any</span></span>|<span data-ttu-id="53652-554">원본 배열의 각 요소에 적용할 프로젝션입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-554">The projection to apply to each element of the source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="53652-555">종료 작업</span><span class="sxs-lookup"><span data-stu-id="53652-555">Terminate action</span></span>

<span data-ttu-id="53652-556">종료 작업은 진행 중인 작업을 중단하고 나머지 작업을 건너뛰어 워크플로 실행을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="53652-557">예를 들어 **실패** 상태의 실행을 종료하려면 다음 코드 조각을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="53652-558">이미 완료된 작업은 종료 작업에 의해 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-558">Actions already completed are not affected by the terminate action.</span></span>

|<span data-ttu-id="53652-559">이름</span><span class="sxs-lookup"><span data-stu-id="53652-559">Name</span></span>|<span data-ttu-id="53652-560">필수</span><span class="sxs-lookup"><span data-stu-id="53652-560">Required</span></span>|<span data-ttu-id="53652-561">형식</span><span class="sxs-lookup"><span data-stu-id="53652-561">Type</span></span>|<span data-ttu-id="53652-562">설명</span><span class="sxs-lookup"><span data-stu-id="53652-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="53652-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="53652-563">runStatus</span></span>|<span data-ttu-id="53652-564">예</span><span class="sxs-lookup"><span data-stu-id="53652-564">Yes</span></span>|<span data-ttu-id="53652-565">string</span><span class="sxs-lookup"><span data-stu-id="53652-565">String</span></span>|<span data-ttu-id="53652-566">커넥터 실행 상태</span><span class="sxs-lookup"><span data-stu-id="53652-566">The target run status.</span></span> <span data-ttu-id="53652-567">**Failed** 또는 **Cancelled**입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="53652-568">runError</span><span class="sxs-lookup"><span data-stu-id="53652-568">runError</span></span>|<span data-ttu-id="53652-569">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-569">No</span></span>|<span data-ttu-id="53652-570">Object</span><span class="sxs-lookup"><span data-stu-id="53652-570">Object</span></span>|<span data-ttu-id="53652-571">오류 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-571">The error details.</span></span> <span data-ttu-id="53652-572">**runStatus**가 **Failed**로 설정된 경우에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-572">Only supported when **runStatus** is set to **Failed**.</span></span>|
|<span data-ttu-id="53652-573">runError code</span><span class="sxs-lookup"><span data-stu-id="53652-573">runError code</span></span>|<span data-ttu-id="53652-574">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-574">No</span></span>|<span data-ttu-id="53652-575">문자열</span><span class="sxs-lookup"><span data-stu-id="53652-575">String</span></span>|<span data-ttu-id="53652-576">실행 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-576">The run error code.</span></span>|
|<span data-ttu-id="53652-577">runError message</span><span class="sxs-lookup"><span data-stu-id="53652-577">runError message</span></span>|<span data-ttu-id="53652-578">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-578">No</span></span>|<span data-ttu-id="53652-579">문자열</span><span class="sxs-lookup"><span data-stu-id="53652-579">String</span></span>|<span data-ttu-id="53652-580">실행 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-580">The run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="53652-581">작성 작업</span><span class="sxs-lookup"><span data-stu-id="53652-581">Compose action</span></span>

<span data-ttu-id="53652-582">작성 작업을 통해 임의 개체를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-582">The Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="53652-583">작성 작업의 출력은 해당 입력을 평가한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-583">The output of the compose action is the result of evaluating its inputs.</span></span> <span data-ttu-id="53652-584">예를 들어 작성 작업을 사용하여 여러 작업의 출력을 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-584">For example, you can use the compose action to merge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="53652-585">**작성** 작업은 개체, 배열 및 논리 앱에서 기본적으로 지원하는 기타 형식(XML 및 이진)을 포함한 출력을 생성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="53652-586">테이블 작업</span><span class="sxs-lookup"><span data-stu-id="53652-586">Table action</span></span>

<span data-ttu-id="53652-587">`table`을 사용하면 항목의 배열을 **CSV** 또는 **HTML** 테이블로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-587">The `table` allows you to convert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="53652-588">@triggerBody()을 다음으로 가정합니다</span><span class="sxs-lookup"><span data-stu-id="53652-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="53652-589">작업이 다음으로 정의되게 합니다</span><span class="sxs-lookup"><span data-stu-id="53652-589">And let the action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="53652-590">위의 내용은 다음을 생성합니다</span><span class="sxs-lookup"><span data-stu-id="53652-590">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="53652-591">id</span><span class="sxs-lookup"><span data-stu-id="53652-591">id</span></span></th><th><span data-ttu-id="53652-592">name</span><span class="sxs-lookup"><span data-stu-id="53652-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="53652-593">0</span><span class="sxs-lookup"><span data-stu-id="53652-593">0</span></span></td><td><span data-ttu-id="53652-594">사과</span><span class="sxs-lookup"><span data-stu-id="53652-594">apples</span></span></td></tr><tr><td><span data-ttu-id="53652-595">1</span><span class="sxs-lookup"><span data-stu-id="53652-595">1</span></span></td><td><span data-ttu-id="53652-596">오렌지</span><span class="sxs-lookup"><span data-stu-id="53652-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="53652-597">"</span><span class="sxs-lookup"><span data-stu-id="53652-597">"</span></span>

<span data-ttu-id="53652-598">테이블을 사용자 지정하려면 열을 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-598">In order to customize the table, you can specify the columns explicitly.</span></span> <span data-ttu-id="53652-599">예:</span><span class="sxs-lookup"><span data-stu-id="53652-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="53652-600">위의 내용은 다음을 생성합니다</span><span class="sxs-lookup"><span data-stu-id="53652-600">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="53652-601">ID를 생성합니다</span><span class="sxs-lookup"><span data-stu-id="53652-601">produce id</span></span></th><th><span data-ttu-id="53652-602">설명</span><span class="sxs-lookup"><span data-stu-id="53652-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="53652-603">0</span><span class="sxs-lookup"><span data-stu-id="53652-603">0</span></span></td><td><span data-ttu-id="53652-604">신선한 사과</span><span class="sxs-lookup"><span data-stu-id="53652-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="53652-605">1</span><span class="sxs-lookup"><span data-stu-id="53652-605">1</span></span></td><td><span data-ttu-id="53652-606">신선한 오렌지</span><span class="sxs-lookup"><span data-stu-id="53652-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="53652-607">"</span><span class="sxs-lookup"><span data-stu-id="53652-607">"</span></span>

<span data-ttu-id="53652-608">`from` 속성 값이 빈 배열인 경우 출력도 빈 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-608">If the `from` property value is an empty array, the output is an empty table.</span></span>

|<span data-ttu-id="53652-609">이름</span><span class="sxs-lookup"><span data-stu-id="53652-609">Name</span></span>|<span data-ttu-id="53652-610">필수</span><span class="sxs-lookup"><span data-stu-id="53652-610">Required</span></span>|<span data-ttu-id="53652-611">형식</span><span class="sxs-lookup"><span data-stu-id="53652-611">Type</span></span>|<span data-ttu-id="53652-612">설명</span><span class="sxs-lookup"><span data-stu-id="53652-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="53652-613">from</span><span class="sxs-lookup"><span data-stu-id="53652-613">from</span></span>|<span data-ttu-id="53652-614">예</span><span class="sxs-lookup"><span data-stu-id="53652-614">Yes</span></span>|<span data-ttu-id="53652-615">배열</span><span class="sxs-lookup"><span data-stu-id="53652-615">Array</span></span>|<span data-ttu-id="53652-616">원본 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-616">The source array.</span></span>|
|<span data-ttu-id="53652-617">format</span><span class="sxs-lookup"><span data-stu-id="53652-617">format</span></span>|<span data-ttu-id="53652-618">예</span><span class="sxs-lookup"><span data-stu-id="53652-618">Yes</span></span>|<span data-ttu-id="53652-619">문자열</span><span class="sxs-lookup"><span data-stu-id="53652-619">String</span></span>|<span data-ttu-id="53652-620">형식은 **CSV** 또는 **HTML**입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-620">The format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="53652-621">열</span><span class="sxs-lookup"><span data-stu-id="53652-621">columns</span></span>|<span data-ttu-id="53652-622">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-622">No</span></span>|<span data-ttu-id="53652-623">배열</span><span class="sxs-lookup"><span data-stu-id="53652-623">Array</span></span>|<span data-ttu-id="53652-624">열입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-624">The columns.</span></span> <span data-ttu-id="53652-625">테이블의 기본 셰이프를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-625">Allows to override the default shape of the table.</span></span>|
|<span data-ttu-id="53652-626">열 머리글</span><span class="sxs-lookup"><span data-stu-id="53652-626">column header</span></span>|<span data-ttu-id="53652-627">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-627">No</span></span>|<span data-ttu-id="53652-628">string</span><span class="sxs-lookup"><span data-stu-id="53652-628">String</span></span>|<span data-ttu-id="53652-629">열의 머리글입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-629">The header of the column.</span></span>|
|<span data-ttu-id="53652-630">열 값</span><span class="sxs-lookup"><span data-stu-id="53652-630">column value</span></span>|<span data-ttu-id="53652-631">예</span><span class="sxs-lookup"><span data-stu-id="53652-631">Yes</span></span>|<span data-ttu-id="53652-632">String</span><span class="sxs-lookup"><span data-stu-id="53652-632">String</span></span>|<span data-ttu-id="53652-633">열의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-633">The value of the column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="53652-634">워크플로 작업</span><span class="sxs-lookup"><span data-stu-id="53652-634">Workflow action</span></span>   

|<span data-ttu-id="53652-635">이름</span><span class="sxs-lookup"><span data-stu-id="53652-635">Name</span></span>|<span data-ttu-id="53652-636">필수</span><span class="sxs-lookup"><span data-stu-id="53652-636">Required</span></span>|<span data-ttu-id="53652-637">형식</span><span class="sxs-lookup"><span data-stu-id="53652-637">Type</span></span>|<span data-ttu-id="53652-638">설명</span><span class="sxs-lookup"><span data-stu-id="53652-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="53652-639">host id</span><span class="sxs-lookup"><span data-stu-id="53652-639">host id</span></span>|<span data-ttu-id="53652-640">예</span><span class="sxs-lookup"><span data-stu-id="53652-640">Yes</span></span>|<span data-ttu-id="53652-641">String</span><span class="sxs-lookup"><span data-stu-id="53652-641">String</span></span>|<span data-ttu-id="53652-642">호출할 워크플로의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-642">The resource ID of the workflow that you want to call.</span></span>|  
|<span data-ttu-id="53652-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="53652-643">host triggerName</span></span>|<span data-ttu-id="53652-644">예</span><span class="sxs-lookup"><span data-stu-id="53652-644">Yes</span></span>|<span data-ttu-id="53652-645">String</span><span class="sxs-lookup"><span data-stu-id="53652-645">String</span></span>|<span data-ttu-id="53652-646">호출할 트리거의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-646">The name of the trigger that you want to invoke.</span></span>|  
|<span data-ttu-id="53652-647">쿼리</span><span class="sxs-lookup"><span data-stu-id="53652-647">queries</span></span>|<span data-ttu-id="53652-648">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-648">No</span></span>|<span data-ttu-id="53652-649">Object</span><span class="sxs-lookup"><span data-stu-id="53652-649">Object</span></span>|<span data-ttu-id="53652-650">URL에 추가할 쿼리 매개 변수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-650">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="53652-651">예를 들어 `"queries" : { "api-version": "2015-02-01" }`은 URL에 `?api-version=2015-02-01`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="53652-652">headers</span><span class="sxs-lookup"><span data-stu-id="53652-652">headers</span></span>|<span data-ttu-id="53652-653">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-653">No</span></span>|<span data-ttu-id="53652-654">Object</span><span class="sxs-lookup"><span data-stu-id="53652-654">Object</span></span>|<span data-ttu-id="53652-655">요청에 전송된 각 헤더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-655">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="53652-656">예를 들어 요청에 언어 및 형식을 설정하려면 다음과 같이 합니다. `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="53652-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="53652-657">body</span><span class="sxs-lookup"><span data-stu-id="53652-657">body</span></span>|<span data-ttu-id="53652-658">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-658">No</span></span>|<span data-ttu-id="53652-659">Object</span><span class="sxs-lookup"><span data-stu-id="53652-659">Object</span></span>|<span data-ttu-id="53652-660">끝점에 전송된 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-660">Represents the payload sent to the endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="53652-661">워크플로\(보다 구체적으로 트리거\)에 대해 액세스 검사가 이루어지므로 워크플로에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span></span>  
  
<span data-ttu-id="53652-662">`workflow` 작업의 출력은 하위 워크플로에서 `response` 작업에 정의된 내용을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span></span> <span data-ttu-id="53652-663">어떤 `response` 작업도 정의되지 않은 경우 출력은 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-663">If you have not defined any `response` action, then the outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="53652-664">Function 작업</span><span class="sxs-lookup"><span data-stu-id="53652-664">Function action</span></span>   

|<span data-ttu-id="53652-665">이름</span><span class="sxs-lookup"><span data-stu-id="53652-665">Name</span></span>|<span data-ttu-id="53652-666">필수</span><span class="sxs-lookup"><span data-stu-id="53652-666">Required</span></span>|<span data-ttu-id="53652-667">형식</span><span class="sxs-lookup"><span data-stu-id="53652-667">Type</span></span>|<span data-ttu-id="53652-668">설명</span><span class="sxs-lookup"><span data-stu-id="53652-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="53652-669">function id</span><span class="sxs-lookup"><span data-stu-id="53652-669">function id</span></span>|<span data-ttu-id="53652-670">예</span><span class="sxs-lookup"><span data-stu-id="53652-670">Yes</span></span>|<span data-ttu-id="53652-671">string</span><span class="sxs-lookup"><span data-stu-id="53652-671">String</span></span>|<span data-ttu-id="53652-672">호출하려는 함수의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-672">The resource ID of the function that you want to invoke.</span></span>|  
|<span data-ttu-id="53652-673">메서드</span><span class="sxs-lookup"><span data-stu-id="53652-673">method</span></span>|<span data-ttu-id="53652-674">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-674">No</span></span>|<span data-ttu-id="53652-675">string</span><span class="sxs-lookup"><span data-stu-id="53652-675">String</span></span>|<span data-ttu-id="53652-676">함수를 호출하는 데 사용되는 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-676">The HTTP method used to invoke the function.</span></span> <span data-ttu-id="53652-677">기본적으로 지정되지 않은 경우 `POST`입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="53652-678">쿼리</span><span class="sxs-lookup"><span data-stu-id="53652-678">queries</span></span>|<span data-ttu-id="53652-679">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-679">No</span></span>|<span data-ttu-id="53652-680">Object</span><span class="sxs-lookup"><span data-stu-id="53652-680">Object</span></span>|<span data-ttu-id="53652-681">URL에 추가할 쿼리 매개 변수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-681">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="53652-682">예를 들어 `"queries" : { "api-version": "2015-02-01" }`은 URL에 `?api-version=2015-02-01`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="53652-683">headers</span><span class="sxs-lookup"><span data-stu-id="53652-683">headers</span></span>|<span data-ttu-id="53652-684">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-684">No</span></span>|<span data-ttu-id="53652-685">Object</span><span class="sxs-lookup"><span data-stu-id="53652-685">Object</span></span>|<span data-ttu-id="53652-686">요청에 전송된 각 헤더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-686">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="53652-687">예를 들어 요청에 언어 및 형식을 설정하려면 다음과 같이 합니다. `"headers" : { "Accept-Language": "en-us" }`</span><span class="sxs-lookup"><span data-stu-id="53652-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="53652-688">body</span><span class="sxs-lookup"><span data-stu-id="53652-688">body</span></span>|<span data-ttu-id="53652-689">아니요</span><span class="sxs-lookup"><span data-stu-id="53652-689">No</span></span>|<span data-ttu-id="53652-690">Object</span><span class="sxs-lookup"><span data-stu-id="53652-690">Object</span></span>|<span data-ttu-id="53652-691">끝점에 전송된 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53652-691">Represents the payload sent to the endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="53652-692">논리 앱을 저장하는 경우 참조된 함수에 대한 몇 가지 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-692">When you save the logic app, we perform some checks on the referenced function:</span></span>
-   <span data-ttu-id="53652-693">함수에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-693">You need to have access to the function.</span></span>
-   <span data-ttu-id="53652-694">표준 HTTP 트리거 또는 일반 JSON 웹후크 트리거만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="53652-695">경로를 정의하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="53652-696">"함수" 및 "익명" 권한 부여 수준만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="53652-697">트리거 URL은 런타임에 검색, 캐시 및 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-697">The trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="53652-698">따라서 어떤 작업으로 캐시된 URL이 무효화되면 런타임에 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-698">So if any operation invalidates the cached URL, the action fails at runtime.</span></span> <span data-ttu-id="53652-699">이 문제를 해결하려면 논리 앱을 다시 저장합니다. 그러면 논리 앱이 트리거 URL을 다시 검색하고 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="53652-700">컬렉션 작업(범위 및 루프)</span><span class="sxs-lookup"><span data-stu-id="53652-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="53652-701">일부 작업 유형은 자체 내에 작업을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="53652-702">컬렉션 내에서 참조 작업은 컬렉션 외부에서 직접 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-702">Reference actions within a collection can be referenced directly outside of the collection.</span></span> <span data-ttu-id="53652-703">범위에 `http`를 정의한 경우 `@body('http')`는 워크플로 어느 곳에서나 여전히 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="53652-704">컬렉션 내에 있는 작업은 동일한 컬렉션 내에 있는 다른 작업만 `runAfter`할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-704">Actions within a collection can `runAfter` only other actions within the same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="53652-705">범위 작업</span><span class="sxs-lookup"><span data-stu-id="53652-705">Scope action</span></span>

<span data-ttu-id="53652-706">`scope` 작업을 통해 워크플로에서 작업을 논리적으로 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-706">The `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="53652-707">이름</span><span class="sxs-lookup"><span data-stu-id="53652-707">Name</span></span>|<span data-ttu-id="53652-708">필수</span><span class="sxs-lookup"><span data-stu-id="53652-708">Required</span></span>|<span data-ttu-id="53652-709">형식</span><span class="sxs-lookup"><span data-stu-id="53652-709">Type</span></span>|<span data-ttu-id="53652-710">설명</span><span class="sxs-lookup"><span data-stu-id="53652-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="53652-711">actions</span><span class="sxs-lookup"><span data-stu-id="53652-711">actions</span></span>|<span data-ttu-id="53652-712">예</span><span class="sxs-lookup"><span data-stu-id="53652-712">Yes</span></span>|<span data-ttu-id="53652-713">Object</span><span class="sxs-lookup"><span data-stu-id="53652-713">Object</span></span>|<span data-ttu-id="53652-714">범위 내에서 실행할 내부 작업</span><span class="sxs-lookup"><span data-stu-id="53652-714">Inner actions to execute within the scope</span></span>|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a><span data-ttu-id="53652-715">ForEach 작업</span><span class="sxs-lookup"><span data-stu-id="53652-715">ForEach action</span></span>

<span data-ttu-id="53652-716">이 루프 작업은 배열을 반복하고 각 항목에 대해 내부 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="53652-717">기본적으로 foreach 루프는 병렬로 실행됩니다(한 번에 20개 실행을 병렬로 수행).</span><span class="sxs-lookup"><span data-stu-id="53652-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="53652-718">`operationOptions` 매개 변수를 사용하여 실행 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-718">You can set execution rules using the `operationOptions` parameter.</span></span>

|<span data-ttu-id="53652-719">이름</span><span class="sxs-lookup"><span data-stu-id="53652-719">Name</span></span>|<span data-ttu-id="53652-720">필수</span><span class="sxs-lookup"><span data-stu-id="53652-720">Required</span></span>|<span data-ttu-id="53652-721">형식</span><span class="sxs-lookup"><span data-stu-id="53652-721">Type</span></span>|<span data-ttu-id="53652-722">설명</span><span class="sxs-lookup"><span data-stu-id="53652-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="53652-723">actions</span><span class="sxs-lookup"><span data-stu-id="53652-723">actions</span></span>|<span data-ttu-id="53652-724">예</span><span class="sxs-lookup"><span data-stu-id="53652-724">Yes</span></span>|<span data-ttu-id="53652-725">Object</span><span class="sxs-lookup"><span data-stu-id="53652-725">Object</span></span>|<span data-ttu-id="53652-726">루프 내에서 실행할 내부 작업</span><span class="sxs-lookup"><span data-stu-id="53652-726">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="53652-727">foreach</span><span class="sxs-lookup"><span data-stu-id="53652-727">foreach</span></span>|<span data-ttu-id="53652-728">예</span><span class="sxs-lookup"><span data-stu-id="53652-728">Yes</span></span>|<span data-ttu-id="53652-729">string</span><span class="sxs-lookup"><span data-stu-id="53652-729">string</span></span>|<span data-ttu-id="53652-730">반복할 배열</span><span class="sxs-lookup"><span data-stu-id="53652-730">The array to iterate over</span></span>|
|<span data-ttu-id="53652-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="53652-731">operationOptions</span></span>|<span data-ttu-id="53652-732">no</span><span class="sxs-lookup"><span data-stu-id="53652-732">no</span></span>|<span data-ttu-id="53652-733">string</span><span class="sxs-lookup"><span data-stu-id="53652-733">string</span></span>|<span data-ttu-id="53652-734">동작에 대한 모든 작업 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-734">Any operation options for behavior.</span></span> <span data-ttu-id="53652-735">현재는 반복을 순차적으로 실행하는 `sequential`만 지원합니다(기본 동작은 병렬).</span><span class="sxs-lookup"><span data-stu-id="53652-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span></span>|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="53652-736">Until 작업</span><span class="sxs-lookup"><span data-stu-id="53652-736">Until action</span></span>

<span data-ttu-id="53652-737">이 루프 작업은 조건 결과가 true일 때까지 내부 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-737">This looping action executes inner actions until a condition results to true.</span></span>

|<span data-ttu-id="53652-738">이름</span><span class="sxs-lookup"><span data-stu-id="53652-738">Name</span></span>|<span data-ttu-id="53652-739">필수</span><span class="sxs-lookup"><span data-stu-id="53652-739">Required</span></span>|<span data-ttu-id="53652-740">형식</span><span class="sxs-lookup"><span data-stu-id="53652-740">Type</span></span>|<span data-ttu-id="53652-741">설명</span><span class="sxs-lookup"><span data-stu-id="53652-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="53652-742">actions</span><span class="sxs-lookup"><span data-stu-id="53652-742">actions</span></span>|<span data-ttu-id="53652-743">예</span><span class="sxs-lookup"><span data-stu-id="53652-743">Yes</span></span>|<span data-ttu-id="53652-744">Object</span><span class="sxs-lookup"><span data-stu-id="53652-744">Object</span></span>|<span data-ttu-id="53652-745">루프 내에서 실행할 내부 작업</span><span class="sxs-lookup"><span data-stu-id="53652-745">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="53652-746">식</span><span class="sxs-lookup"><span data-stu-id="53652-746">expression</span></span>|<span data-ttu-id="53652-747">예</span><span class="sxs-lookup"><span data-stu-id="53652-747">Yes</span></span>|<span data-ttu-id="53652-748">string</span><span class="sxs-lookup"><span data-stu-id="53652-748">string</span></span>|<span data-ttu-id="53652-749">각 반복 후마다 평가할 식</span><span class="sxs-lookup"><span data-stu-id="53652-749">The expression to evaluate after each iteration</span></span>|
|<span data-ttu-id="53652-750">limit</span><span class="sxs-lookup"><span data-stu-id="53652-750">limit</span></span>|<span data-ttu-id="53652-751">yes</span><span class="sxs-lookup"><span data-stu-id="53652-751">yes</span></span>|<span data-ttu-id="53652-752">Object</span><span class="sxs-lookup"><span data-stu-id="53652-752">Object</span></span>|<span data-ttu-id="53652-753">루프에 대한 제한 - 제한을 하나 이상 정의해야 함</span><span class="sxs-lookup"><span data-stu-id="53652-753">The limits for the loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="53652-754">count</span><span class="sxs-lookup"><span data-stu-id="53652-754">count</span></span>|<span data-ttu-id="53652-755">no</span><span class="sxs-lookup"><span data-stu-id="53652-755">no</span></span>|<span data-ttu-id="53652-756">int</span><span class="sxs-lookup"><span data-stu-id="53652-756">int</span></span>|<span data-ttu-id="53652-757">수행할 수 있는 반복 수에 대한 제한</span><span class="sxs-lookup"><span data-stu-id="53652-757">The limit to the number of iterations that can be performed</span></span>|
|<span data-ttu-id="53652-758">시간 제한</span><span class="sxs-lookup"><span data-stu-id="53652-758">timeout</span></span>|<span data-ttu-id="53652-759">no</span><span class="sxs-lookup"><span data-stu-id="53652-759">no</span></span>|<span data-ttu-id="53652-760">string</span><span class="sxs-lookup"><span data-stu-id="53652-760">string</span></span>|<span data-ttu-id="53652-761">반복 기간에 대한 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="53652-761">The timeout for how long it should loop.</span></span>  <span data-ttu-id="53652-762">ISO 8601 형식</span><span class="sxs-lookup"><span data-stu-id="53652-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="53652-763">조건 - If 작업</span><span class="sxs-lookup"><span data-stu-id="53652-763">Conditions - If Action</span></span>

<span data-ttu-id="53652-764">`If` 작업을 통해 조건을 평가하고 식이 `true`로 평가되는지 여부에 따라 분기를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span></span>

|<span data-ttu-id="53652-765">이름</span><span class="sxs-lookup"><span data-stu-id="53652-765">Name</span></span>|<span data-ttu-id="53652-766">필수</span><span class="sxs-lookup"><span data-stu-id="53652-766">Required</span></span>|<span data-ttu-id="53652-767">형식</span><span class="sxs-lookup"><span data-stu-id="53652-767">Type</span></span>|<span data-ttu-id="53652-768">설명</span><span class="sxs-lookup"><span data-stu-id="53652-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="53652-769">actions</span><span class="sxs-lookup"><span data-stu-id="53652-769">actions</span></span>|<span data-ttu-id="53652-770">예</span><span class="sxs-lookup"><span data-stu-id="53652-770">Yes</span></span>|<span data-ttu-id="53652-771">Object</span><span class="sxs-lookup"><span data-stu-id="53652-771">Object</span></span>|<span data-ttu-id="53652-772">식이 `true`로 평가될 때 실행할 내부 작업</span><span class="sxs-lookup"><span data-stu-id="53652-772">Inner actions to execute when expression evaluates to `true`</span></span>|
|<span data-ttu-id="53652-773">식</span><span class="sxs-lookup"><span data-stu-id="53652-773">expression</span></span>|<span data-ttu-id="53652-774">예</span><span class="sxs-lookup"><span data-stu-id="53652-774">Yes</span></span>|<span data-ttu-id="53652-775">string</span><span class="sxs-lookup"><span data-stu-id="53652-775">string</span></span>|<span data-ttu-id="53652-776">평가할 식</span><span class="sxs-lookup"><span data-stu-id="53652-776">The expression to evaluate</span></span>|
|<span data-ttu-id="53652-777">else</span><span class="sxs-lookup"><span data-stu-id="53652-777">else</span></span>|<span data-ttu-id="53652-778">no</span><span class="sxs-lookup"><span data-stu-id="53652-778">no</span></span>|<span data-ttu-id="53652-779">Object</span><span class="sxs-lookup"><span data-stu-id="53652-779">Object</span></span>|<span data-ttu-id="53652-780">식이 `false`로 평가될 때 실행할 내부 작업</span><span class="sxs-lookup"><span data-stu-id="53652-780">Inner actions to execute when expression evaluates to `false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="53652-781">다음 표에서는 조건에서 작업에 식을 사용하는 방법에 대한 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="53652-781">The following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="53652-782">JSON 값</span><span class="sxs-lookup"><span data-stu-id="53652-782">JSON value</span></span>|<span data-ttu-id="53652-783">결과</span><span class="sxs-lookup"><span data-stu-id="53652-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="53652-784">true로 평가되는 모든 값을 통해 이 조건을 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-784">Any value that would evaluate to true causes this condition to pass.</span></span> <span data-ttu-id="53652-785">부울 식만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="53652-786">다른 형식을 부울로 변환하려면 `empty`, `equals` 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53652-786">To convert other types to Boolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="53652-787">비교 함수는 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-787">Comparison functions are supported.</span></span> <span data-ttu-id="53652-788">여기에 표시된 예제에서는 act1의 출력이 임계값보다 큰 경우에만 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="53652-789">중첩된 부울 식을 만들기 위해 논리 함수도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-789">Logic functions are also supported to create nested Boolean expressions.</span></span> <span data-ttu-id="53652-790">이 경우 act1의 출력이 임계값보다 크거나 100 미만인 경우 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="53652-791">배열 함수를 사용하여 배열에 항목이 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53652-791">You can use array functions to check if an array has any items.</span></span> <span data-ttu-id="53652-792">이 경우 오류 배열이 비어 있으면 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-792">In this case, the action executes when the errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="53652-793">오류 - 조건에 @이 필요하므로 유효한 조건이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="53652-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="53652-794">조건이 성공적으로 평가되면 조건이 `Succeeded`로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span></span> <span data-ttu-id="53652-795">`actions` 또는 `else` 개체 내의 작업이 실행되어 성공하면 `Succeeded`로 평가되고, 실행되어 실패하면 `Failed`로, 분기가 실행되지 않으면 `Skipped`로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="53652-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53652-796">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53652-796">Next steps</span></span>

[<span data-ttu-id="53652-797">워크플로 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="53652-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
