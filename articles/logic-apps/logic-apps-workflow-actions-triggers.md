---
title: "aaaWorkflow 동작 및 트리거-Azure 논리 앱 | Microsoft Docs"
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
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="c453a-102">Azure Logic Apps의 워크플로 작업 및 트리거</span><span class="sxs-lookup"><span data-stu-id="c453a-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="c453a-103">논리 앱은 트리거와 작업으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="c453a-104">트리거에는 여섯 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-104">There are six types of triggers.</span></span> <span data-ttu-id="c453a-105">각 유형마다 서로 다른 인터페이스 및 동작을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="c453a-106">Hello의 hello 세부 정보를 확인 하 여 다른 세부 정보에 대해 알아볼 수 있습니다 [워크플로 정의 언어](logic-apps-workflow-definition-language.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="c453a-107">비즈니스 프로세스와 워크플로 트리거 및 동작 사용 하는 방법으로 toobuild 논리 앱 tooimprove에 대해 자세히 toolearn 계속 읽어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="c453a-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="c453a-108">트리거</span><span class="sxs-lookup"><span data-stu-id="c453a-108">Triggers</span></span>  

<span data-ttu-id="c453a-109">트리거 논리 앱 워크플로 실행을 시작할 수 있는 hello 호출을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="c453a-110">Hello 두 가지 방법으로 tooinitiate 워크플로 실행 하는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="c453a-111">폴링 트리거</span><span class="sxs-lookup"><span data-stu-id="c453a-111">A polling trigger</span></span>  

-   <span data-ttu-id="c453a-112">Hello 호출 하 여 밀어넣기 트리거- [워크플로 서비스 REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="c453a-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="c453a-113">모든 트리거는 다음과 같은 상위 수준 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="c453a-114">트리거 유형 및 해당 입력</span><span class="sxs-lookup"><span data-stu-id="c453a-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="c453a-115">다음과 같은 트리거 유형을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="c453a-116">**요청** \- toocall 있습니다에 대 한 끝점 hello 논리 앱을 사용 하면</span><span class="sxs-lookup"><span data-stu-id="c453a-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="c453a-117">**Recurrence** \- 정의된 일정에 따라 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="c453a-118">**HTTP** \- HTTP 웹 끝점을 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="c453a-119">hello HTTP 끝점 tooa 특정 트리거 계약을 준수 해야 \- 202를 사용 하 여\-비동기 패턴 또는 배열을 반환 하 여</span><span class="sxs-lookup"><span data-stu-id="c453a-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="c453a-120">**그러나 ApiConnection** \- 설문 hello HTTP와 같은 트리거, 이용할 hello [Microsoft 관리 Api](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="c453a-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="c453a-121">**그러나 HTTPWebhook** \- 끝점의 경우 유사한 toohello 수동 트리거가 호출 tooa 아웃 URL tooregister 지정 및 등록 취소</span><span class="sxs-lookup"><span data-stu-id="c453a-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="c453a-122">**ApiConnectionWebhook** \- HTTPWebhook 트리거 hello Microsoft 관리 Api 활용 하 여 hello 처럼 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="c453a-123">각 트리거 형식은 해당 동작을 정의하는 서로 다른 **입력** 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="c453a-124">요청 트리거</span><span class="sxs-lookup"><span data-stu-id="c453a-124">Request trigger</span></span>  

<span data-ttu-id="c453a-125">이 트리거 논리 앱을 통해 HTTP 요청 tooinvoke 호출 하는 끝점으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="c453a-126">요청 트리거는 다음 예제와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-126">A request trigger looks like this example:</span></span>  
  
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

<span data-ttu-id="c453a-127">또한 **schema**라는 선택적 속성도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="c453a-128">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-128">Element name</span></span>|<span data-ttu-id="c453a-129">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-129">Required</span></span>|<span data-ttu-id="c453a-130">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="c453a-131">schema</span><span class="sxs-lookup"><span data-stu-id="c453a-131">schema</span></span>|<span data-ttu-id="c453a-132">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-132">No</span></span>|<span data-ttu-id="c453a-133">Hello 들어오는 요청을 확인 하는 JSON 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="c453a-134">이후 워크플로 단계 알고 있는 속성 tooreference 수 있도록 지 원하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="c453a-135">tooinvoke이이 끝점 toocall hello 해야 *listCallbackUrl* API입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="c453a-136">[워크플로 서비스 REST API](https://docs.microsoft.com/rest/api/logic/workflows)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c453a-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="c453a-137">되풀이 트리거</span><span class="sxs-lookup"><span data-stu-id="c453a-137">Recurrence trigger</span></span>  

<span data-ttu-id="c453a-138">되풀이 트리거는 정의된 일정에 따라 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="c453a-139">이러한 트리거는 다음 예제와 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="c453a-140">볼 수 있듯이 간단한 방법을 toorun 워크플로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="c453a-141">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-141">Element name</span></span>|<span data-ttu-id="c453a-142">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-142">Required</span></span>|<span data-ttu-id="c453a-143">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="c453a-144">frequency</span><span class="sxs-lookup"><span data-stu-id="c453a-144">frequency</span></span>|<span data-ttu-id="c453a-145">예</span><span class="sxs-lookup"><span data-stu-id="c453a-145">Yes</span></span>|<span data-ttu-id="c453a-146">얼마나 자주 hello 트리거 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-146">How often hello trigger executes.</span></span> <span data-ttu-id="c453a-147">second, minute, hour, day, week, month 또는 year 중에 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="c453a-148">interval</span><span class="sxs-lookup"><span data-stu-id="c453a-148">interval</span></span>|<span data-ttu-id="c453a-149">예</span><span class="sxs-lookup"><span data-stu-id="c453a-149">Yes</span></span>|<span data-ttu-id="c453a-150">Hello 되풀이 빈도 지정 하는 hello의 간격</span><span class="sxs-lookup"><span data-stu-id="c453a-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="c453a-151">startTime</span><span class="sxs-lookup"><span data-stu-id="c453a-151">startTime</span></span>|<span data-ttu-id="c453a-152">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-152">No</span></span>|<span data-ttu-id="c453a-153">UTC 오프셋 없이 startTime이 제공될 경우 이 timeZone이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="c453a-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="c453a-154">timeZone</span></span>|<span data-ttu-id="c453a-155">no</span><span class="sxs-lookup"><span data-stu-id="c453a-155">no</span></span>|<span data-ttu-id="c453a-156">UTC 오프셋 없이 startTime이 제공될 경우 이 timeZone이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="c453a-157">특정 시점 이후 hello에서 트리거 toostart 실행을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="c453a-158">예를 들어 toostart 주 단위 매주 월요일을 보고 하려는 경우 예약할 수 있습니다 hello 논리 앱 toostart 매주 월요일 hello 다음 트리거를 만들어:</span><span class="sxs-lookup"><span data-stu-id="c453a-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

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

## <a name="http-trigger"></a><span data-ttu-id="c453a-159">HTTP 트리거</span><span class="sxs-lookup"><span data-stu-id="c453a-159">HTTP trigger</span></span>  

<span data-ttu-id="c453a-160">HTTP 트리거 폴링을 지정 된 끝점 및 hello 응답 toodetermine를 hello 워크플로 실행 해야 하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="c453a-161">필요한 tooconstruct HTTP 호출을 매개 변수는 hello 집합을 사용 하는 hello 입력 개체:</span><span class="sxs-lookup"><span data-stu-id="c453a-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="c453a-162">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-162">Element name</span></span>|<span data-ttu-id="c453a-163">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-163">Required</span></span>|<span data-ttu-id="c453a-164">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-164">Description</span></span>|<span data-ttu-id="c453a-165">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="c453a-166">메서드</span><span class="sxs-lookup"><span data-stu-id="c453a-166">method</span></span>|<span data-ttu-id="c453a-167">yes</span><span class="sxs-lookup"><span data-stu-id="c453a-167">yes</span></span>|<span data-ttu-id="c453a-168">Hello HTTP 메서드를 다음 중 하나일 수 있습니다: GET, POST, PUT, DELETE, 패치 또는 H e a d</span><span class="sxs-lookup"><span data-stu-id="c453a-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="c453a-169">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-169">String</span></span>|  
|<span data-ttu-id="c453a-170">uri</span><span class="sxs-lookup"><span data-stu-id="c453a-170">uri</span></span>|<span data-ttu-id="c453a-171">yes</span><span class="sxs-lookup"><span data-stu-id="c453a-171">yes</span></span>|<span data-ttu-id="c453a-172">hello http 또는 https 끝점을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="c453a-173">최대 2킬로바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="c453a-174">string</span><span class="sxs-lookup"><span data-stu-id="c453a-174">String</span></span>|  
|<span data-ttu-id="c453a-175">쿼리</span><span class="sxs-lookup"><span data-stu-id="c453a-175">queries</span></span>|<span data-ttu-id="c453a-176">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-176">No</span></span>|<span data-ttu-id="c453a-177">Hello 쿼리 매개 변수 tooadd toohello URL을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="c453a-178">예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="c453a-179">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-179">Object</span></span>|  
|<span data-ttu-id="c453a-180">headers</span><span class="sxs-lookup"><span data-stu-id="c453a-180">headers</span></span>|<span data-ttu-id="c453a-181">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-181">No</span></span>|<span data-ttu-id="c453a-182">각각의 toohello 요청이 발송 되 hello 머리글을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="c453a-183">예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="c453a-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="c453a-184">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-184">Object</span></span>|  
|<span data-ttu-id="c453a-185">body</span><span class="sxs-lookup"><span data-stu-id="c453a-185">body</span></span>|<span data-ttu-id="c453a-186">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-186">No</span></span>|<span data-ttu-id="c453a-187">Toohello 끝점으로 전송 되는 hello 페이로드를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="c453a-188">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-188">Object</span></span>|  
|<span data-ttu-id="c453a-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="c453a-189">retryPolicy</span></span>|<span data-ttu-id="c453a-190">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-190">No</span></span>|<span data-ttu-id="c453a-191">4xx 또는 5xx 오류에 대 한 hello 다시 시도 동작을 사용자 지정할 수 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="c453a-192">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-192">Object</span></span>|  
|<span data-ttu-id="c453a-193">authentication</span><span class="sxs-lookup"><span data-stu-id="c453a-193">authentication</span></span>|<span data-ttu-id="c453a-194">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-194">No</span></span>|<span data-ttu-id="c453a-195">요청 hello 나타냅니다 hello 메서드를 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="c453a-196">이 개체에 대한 자세한 내용은 [스케줄러 아웃바운드 인증](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c453a-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="c453a-197">스케줄러 이외에도 지원되는 속성이 하나 더 있습니다. `authority` 기본적으로 이 값은 지정되지 않은 경우 `https://login.windows.net`이지만 `https://login.windows\-ppe.net`과 같이 다른 대상 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="c453a-198">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-198">Object</span></span>|  
  
<span data-ttu-id="c453a-199">hello HTTP 트리거 논리 앱 함께 특정 패턴 toowork와 hello HTTP API tooconform이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="c453a-200">다음 필드는 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="c453a-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="c453a-201">응답</span><span class="sxs-lookup"><span data-stu-id="c453a-201">Response</span></span>|<span data-ttu-id="c453a-202">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="c453a-203">상태 코드</span><span class="sxs-lookup"><span data-stu-id="c453a-203">Status code</span></span>|<span data-ttu-id="c453a-204">상태 코드 200 \(확인\) toocause 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="c453a-205">다른 상태 코드이면 실행이 진행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="c453a-206">Retry\-after 헤더</span><span class="sxs-lookup"><span data-stu-id="c453a-206">Retry\-after header</span></span>|<span data-ttu-id="c453a-207">Hello 논리 앱 hello 끝점을 다시 폴링하여 될 때까지 초 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="c453a-208">위치 헤더</span><span class="sxs-lookup"><span data-stu-id="c453a-208">Location header</span></span>|<span data-ttu-id="c453a-209">hello 다음 폴링 간격에 대 한 hello URL toocall 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="c453a-210">지정 하지 않으면 hello 원래 URL이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="c453a-211">다양한 요청 유형의 다양한 동작에 대한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="c453a-212">응답 코드</span><span class="sxs-lookup"><span data-stu-id="c453a-212">Response code</span></span>|<span data-ttu-id="c453a-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="c453a-213">Retry\-After</span></span>|<span data-ttu-id="c453a-214">동작</span><span class="sxs-lookup"><span data-stu-id="c453a-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="c453a-215">200</span><span class="sxs-lookup"><span data-stu-id="c453a-215">200</span></span>|<span data-ttu-id="c453a-216">\(없음\)</span><span class="sxs-lookup"><span data-stu-id="c453a-216">\(none\)</span></span>|<span data-ttu-id="c453a-217">하지 유효한 트리거를 다시 시도\-필수 또는 다른 hello 엔진을는 후 hello 다음 요청에 대 한 폴링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="c453a-218">202</span><span class="sxs-lookup"><span data-stu-id="c453a-218">202</span></span>|<span data-ttu-id="c453a-219">60</span><span class="sxs-lookup"><span data-stu-id="c453a-219">60</span></span>|<span data-ttu-id="c453a-220">Hello 워크플로 트리거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="c453a-221">hello 다음 시도가 1 분 후에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="c453a-222">200</span><span class="sxs-lookup"><span data-stu-id="c453a-222">200</span></span>|<span data-ttu-id="c453a-223">10</span><span class="sxs-lookup"><span data-stu-id="c453a-223">10</span></span>|<span data-ttu-id="c453a-224">Hello 워크플로 실행 하 고 10 초 후에 더 많은 콘텐츠 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="c453a-225">400</span><span class="sxs-lookup"><span data-stu-id="c453a-225">400</span></span>|<span data-ttu-id="c453a-226">\(없음\)</span><span class="sxs-lookup"><span data-stu-id="c453a-226">\(none\)</span></span>|<span data-ttu-id="c453a-227">잘못 된 요청 hello 워크플로 실행 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c453a-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="c453a-228">없는 경우 없는 **을 다시 시도 정책** 정의 hello 기본 정책이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="c453a-229">Hello 재시도 횟수에 도달 하면 hello 트리거를 더 이상 사용할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="c453a-230">500</span><span class="sxs-lookup"><span data-stu-id="c453a-230">500</span></span>|<span data-ttu-id="c453a-231">\(없음\)</span><span class="sxs-lookup"><span data-stu-id="c453a-231">\(none\)</span></span>|<span data-ttu-id="c453a-232">서버 오류를 hello 워크플로 실행 하지 마십시오입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="c453a-233">없는 경우 없는 **을 다시 시도 정책** 정의 hello 기본 정책이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="c453a-234">Hello 재시도 횟수에 도달 하면 hello 트리거를 더 이상 사용할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="c453a-235">hello 출력의 HTTP 트리거는이 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="c453a-236">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-236">Element name</span></span>|<span data-ttu-id="c453a-237">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-237">Description</span></span>|<span data-ttu-id="c453a-238">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="c453a-239">headers</span><span class="sxs-lookup"><span data-stu-id="c453a-239">headers</span></span>|<span data-ttu-id="c453a-240">hello http 응답의 hello 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-240">hello headers of hello http response.</span></span>|<span data-ttu-id="c453a-241">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-241">Object</span></span>|  
|<span data-ttu-id="c453a-242">body</span><span class="sxs-lookup"><span data-stu-id="c453a-242">body</span></span>|<span data-ttu-id="c453a-243">hello http 응답의 hello 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-243">hello body of hello http response.</span></span>|<span data-ttu-id="c453a-244">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="c453a-245">API 연결 트리거</span><span class="sxs-lookup"><span data-stu-id="c453a-245">API Connection trigger</span></span>  

<span data-ttu-id="c453a-246">hello API 연결 트리거는 기본 기능에 비슷한 toohello HTTP 트리거입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="c453a-247">그러나 hello 동작을 식별 하는 것에 대 한 hello 매개 변수는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="c453a-248">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-248">Here is an example:</span></span>  
  
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

|<span data-ttu-id="c453a-249">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-249">Element name</span></span>|<span data-ttu-id="c453a-250">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-250">Required</span></span>|<span data-ttu-id="c453a-251">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-251">Type</span></span>|<span data-ttu-id="c453a-252">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="c453a-253">host</span><span class="sxs-lookup"><span data-stu-id="c453a-253">host</span></span>|<span data-ttu-id="c453a-254">예</span><span class="sxs-lookup"><span data-stu-id="c453a-254">Yes</span></span>||<span data-ttu-id="c453a-255">hello ApiApp 호스팅되는 게이트웨이 및 id입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="c453a-256">메서드</span><span class="sxs-lookup"><span data-stu-id="c453a-256">method</span></span>|<span data-ttu-id="c453a-257">예</span><span class="sxs-lookup"><span data-stu-id="c453a-257">Yes</span></span>|<span data-ttu-id="c453a-258">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-258">String</span></span>|<span data-ttu-id="c453a-259">Hello HTTP 메서드를 다음 중 하나일 수 있습니다: **가져오기**, **POST**, **배치**, **삭제**, **패치**, 또는  **H E A D**</span><span class="sxs-lookup"><span data-stu-id="c453a-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="c453a-260">쿼리</span><span class="sxs-lookup"><span data-stu-id="c453a-260">queries</span></span>|<span data-ttu-id="c453a-261">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-261">No</span></span>|<span data-ttu-id="c453a-262">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-262">Object</span></span>|<span data-ttu-id="c453a-263">나타냅니다 hello 쿼리 매개 변수 toobe toohello URL을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="c453a-264">예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="c453a-265">headers</span><span class="sxs-lookup"><span data-stu-id="c453a-265">headers</span></span>|<span data-ttu-id="c453a-266">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-266">No</span></span>|<span data-ttu-id="c453a-267">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-267">Object</span></span>|<span data-ttu-id="c453a-268">각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="c453a-269">예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="c453a-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="c453a-270">body</span><span class="sxs-lookup"><span data-stu-id="c453a-270">body</span></span>|<span data-ttu-id="c453a-271">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-271">No</span></span>|<span data-ttu-id="c453a-272">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-272">Object</span></span>|<span data-ttu-id="c453a-273">Toohello 끝점으로 전송 되는 hello 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="c453a-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="c453a-274">retryPolicy</span></span>|<span data-ttu-id="c453a-275">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-275">No</span></span>|<span data-ttu-id="c453a-276">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-276">Object</span></span>|<span data-ttu-id="c453a-277">4xx 또는 5xx 오류 toocustomize hello 다시 시도 동작이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="c453a-278">인증</span><span class="sxs-lookup"><span data-stu-id="c453a-278">authentication</span></span>|<span data-ttu-id="c453a-279">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-279">No</span></span>|<span data-ttu-id="c453a-280">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-280">Object</span></span>|<span data-ttu-id="c453a-281">요청 hello 나타냅니다 hello 메서드를 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="c453a-282">이 개체에 대한 자세한 내용은 [스케줄러 아웃바운드 인증](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c453a-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="c453a-283">호스트에 대 한 hello 속성은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="c453a-284">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-284">Element name</span></span>|<span data-ttu-id="c453a-285">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-285">Required</span></span>|<span data-ttu-id="c453a-286">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="c453a-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="c453a-287">api runtimeUrl</span></span>|<span data-ttu-id="c453a-288">예</span><span class="sxs-lookup"><span data-stu-id="c453a-288">Yes</span></span>|<span data-ttu-id="c453a-289">관리 되는 API의 hello hello 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="c453a-290">connection name</span><span class="sxs-lookup"><span data-stu-id="c453a-290">connection name</span></span>||<span data-ttu-id="c453a-291">참조 tooa 매개 변수를 호출 해야 `$connection` hello 워크플로 사용 하 여 관리 하는 hello API 연결의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="c453a-292">API 연결 트리거의 hello 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="c453a-293">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-293">Element name</span></span>|<span data-ttu-id="c453a-294">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-294">Type</span></span>|<span data-ttu-id="c453a-295">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="c453a-296">headers</span><span class="sxs-lookup"><span data-stu-id="c453a-296">headers</span></span>|<span data-ttu-id="c453a-297">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-297">Object</span></span>|<span data-ttu-id="c453a-298">hello http 응답의 hello 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="c453a-299">body</span><span class="sxs-lookup"><span data-stu-id="c453a-299">body</span></span>|<span data-ttu-id="c453a-300">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-300">Object</span></span>|<span data-ttu-id="c453a-301">hello http 응답의 hello 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="c453a-302">HTTPWebhook 트리거</span><span class="sxs-lookup"><span data-stu-id="c453a-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="c453a-303">hello HTTPWebhook 트리거는 끝점, 비슷한 toohello 수동 트리거 있지만 hello HTTPWebhook 트리거 tooa 아웃 계획도 URL tooregister 지정 열리고 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="c453a-304">HTTPWebhook 트리거의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

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

<span data-ttu-id="c453a-305">이 섹션에서는 다양 한 사항이 며 hello Webhook의 hello 동작 섹션을 제공 하거나 생략 됩니다에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="c453a-306">Webhook의 hello 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="c453a-307">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-307">Element name</span></span>|<span data-ttu-id="c453a-308">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-308">Required</span></span>|<span data-ttu-id="c453a-309">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="c453a-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="c453a-310">subscribe</span></span>|<span data-ttu-id="c453a-311">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-311">No</span></span>|<span data-ttu-id="c453a-312">나가는 요청 hello 트리거가 만들어집니다 및 hello 초기 등록을 수행할 때 호출 되는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="c453a-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="c453a-313">unsubscribe</span></span>|<span data-ttu-id="c453a-314">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-314">No</span></span>|<span data-ttu-id="c453a-315">hello hello 트리거를 삭제 요청을 송신 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="c453a-316">**구독** hello toostart 수신 tooevents가 변경한 호출 나갑니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="c453a-317">이 호출이 동일한 일반 HTTP 작업 hello 매개 변수 집합이 않습니다 hello로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="c453a-318">나가는 호출이 만들어진 모든 시간 hello 어떤 방식으로든에서 워크플로 변경 내용을, 예를 들어 때마다 hello 자격 증명을 전달 하는, 또는 hello 트리거의 입력 매개 변수 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="c453a-319">toosupport 호출이 새 함수가: `@listCallbackUrl()`합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="c453a-320">이 함수는 이 워크플로에서 특정 트리거에 대해 고유한 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="c453a-321">Hello hello 서비스 REST를 사용 하는 hello 끝점에 대 한 고유 식별자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="c453a-322">**Unsubscribe**는 다음과 같이 작업에서 이 트리거를 무효화하도록 렌더링할 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="c453a-323">삭제 또는 hello 트리거 비활성화</span><span class="sxs-lookup"><span data-stu-id="c453a-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="c453a-324">삭제 또는 hello 워크플로 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="c453a-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="c453a-325">삭제 하거나 hello 구독 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="c453a-326">hello를 자동으로 호출 하는 hello 논리 앱 작업 구독을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="c453a-327">hello 매개 변수 toothis 함수는 hello HTTP 트리거로 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="c453a-328">hello hello HTTPWebhook 트리거의 출력은 hello 들어오는 요청의 hello 내용을:</span><span class="sxs-lookup"><span data-stu-id="c453a-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="c453a-329">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-329">Element name</span></span>|<span data-ttu-id="c453a-330">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-330">Type</span></span>|<span data-ttu-id="c453a-331">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="c453a-332">headers</span><span class="sxs-lookup"><span data-stu-id="c453a-332">headers</span></span>|<span data-ttu-id="c453a-333">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-333">Object</span></span>|<span data-ttu-id="c453a-334">hello http 요청의 hello 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="c453a-335">body</span><span class="sxs-lookup"><span data-stu-id="c453a-335">body</span></span>|<span data-ttu-id="c453a-336">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-336">Object</span></span>|<span data-ttu-id="c453a-337">hello hello http 요청 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="c453a-338">Hello webhook 작업에 대 한 제한을 지정할 수와 동일 하 게 [HTTP 비동기 제한](#asynchronous-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="c453a-339">조건</span><span class="sxs-lookup"><span data-stu-id="c453a-339">Conditions</span></span>  

<span data-ttu-id="c453a-340">모든 트리거 여부 hello 워크플로 실행 해야 하는지 여부를 하나 이상의 조건 toodetermine를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="c453a-341">예:</span><span class="sxs-lookup"><span data-stu-id="c453a-341">For example:</span></span>  

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

<span data-ttu-id="c453a-342">이 경우 hello 워크플로 하는 동안 보고서만 트리거 hello `sendReports` 매개 변수가 tootrue 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="c453a-343">마지막으로, 조건이 hello 트리거의 hello 상태 코드를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="c453a-344">예를 들어 다음과 같이 웹 사이트에서 상태 코드 500을 반환하는 경우에만 워크플로를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="c453a-345">모든 식 hello 트리거의 hello 상태 코드를 참조 하는 경우 \(어떤 방식으로든에서\), 기본 동작을 hello \(200에 대해서만 트리거 \(확인\) \) 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="c453a-346">예를 들어, 상태 코드 200와 상태 코드 201 tootrigger 원하는 있으면 tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` 조건으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="c453a-347">요청에 대해 여러 실행 시작</span><span class="sxs-lookup"><span data-stu-id="c453a-347">Start multiple runs for a request</span></span>

<span data-ttu-id="c453a-348">단일 요청에 대 한 여러 실행 오프 tookick `splitOn` 유용, 예를 들어 toopoll 폴링 간격 사이 여러 새 항목을 가질 수 있는 끝점을 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="c453a-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="c453a-349">와 `splitOn`, 원하는 각 항목의 hello 배열이 포함 된 hello 응답 페이로드 내 hello 속성 지정 toouse toostart hello 트리거를 실행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="c453a-350">예를 들어 hello 다음 응답을 반환 하는 API가 있는 같이 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
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
  
<span data-ttu-id="c453a-351">논리 앱 하기만 hello 행 콘텐츠이 예제에서와 같이 트리거가 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
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
  
<span data-ttu-id="c453a-352">그런 다음, hello 워크플로 정의 `@triggerBody().name` 반환 `mycoolrow` 를 처음 실행 하는 hello에 대 한 및 `another row` hello 두 번째 실행에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="c453a-353">이 예제에서와 같이 hello 트리거 출력 보기:</span><span class="sxs-lookup"><span data-stu-id="c453a-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="c453a-354">사용 하는 경우에 따라서 `SplitOn`, 외부에 있는 hello 배열에이 예에서 hello hello 속성을 가져올 수 없는 `Status` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="c453a-355">이 예제에서는 사용 하 여 hello `?` 연산자 toobe 수 tooavoid 문제일 경우 hello `Rows` 속성 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="c453a-356">단일 실행 인스턴스</span><span class="sxs-lookup"><span data-stu-id="c453a-356">Single run instance</span></span>

<span data-ttu-id="c453a-357">되풀이 속성 tooonly 화재 되어 모든 활성 실행 완료 하는 경우 트리거를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="c453a-358">예약 된 되풀이 되는 경우 진행 중인 실행 중이면 hello 트리거를 건너뛰어 hello 다음 예약 된 되풀이 간격 toocheck 다시 될 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="c453a-359">Hello 작업 옵션을 통해이 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-359">You can configure this setting through hello operation options:</span></span>

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

## <a name="types-and-inputs"></a><span data-ttu-id="c453a-360">형식 및 입력</span><span class="sxs-lookup"><span data-stu-id="c453a-360">Types and inputs</span></span>  

<span data-ttu-id="c453a-361">다양한 작업 형식이 있으며 각각 고유한 동작을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="c453a-362">컬렉션 작업은 자체적으로 여러 다른 작업을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="c453a-363">표준 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-363">Standard actions</span></span>  

-   <span data-ttu-id="c453a-364">**HTTP** 이 작업은 HTTP 웹 끝점을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="c453a-365">**ApiConnection** \- HTTP 동작 hello와 비슷하게 동작 하는이 작업 이지만 사용 하 여 hello Microsoft에서 관리 하는 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="c453a-366">**ApiConnectionWebhook** \- 같은 HTTPWebhook 하지만 사용 하 여 hello Microsoft 관리 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="c453a-367">**Response** \- 들어오는 호출에 대한 응답을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="c453a-368">**Wait** \- 정해진 시간 동안 기다리거나 특정 시간까지 대기하는 단순한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="c453a-369">**Workflow** \- 중첩된 워크플로를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="c453a-370">**Function** \- 이 작업은 Azure Function을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="c453a-371">컬렉션 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-371">Collection actions</span></span>

-   <span data-ttu-id="c453a-372">**Scope** \- 다른 작업의 논리적 그룹화입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="c453a-373">**조건** \- 이 식을 계산 하는 작업과 hello 해당 결과 분기를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="c453a-374">**ForEach** \- 이 루프 작업은 배열을 반복하고 각 항목에 대해 내부 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="c453a-375">**될 때까지** \- 조건 결과 tootrue 될 때까지이 반복 작업 내부 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="c453a-376">각 작업 형식은 작업의 동작을 정의하는 서로 다른 **입력** 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="c453a-377">HTTP 동작</span><span class="sxs-lookup"><span data-stu-id="c453a-377">HTTP action</span></span>  

<span data-ttu-id="c453a-378">지정 된 끝점을 호출 하 고 hello 워크플로 실행 해야 하는지 여부를 hello 응답 toodetermine를 확인 하는 HTTP 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="c453a-379">hello **입력** 필요한 tooconstruct hello HTTP 호출 매개 변수는 hello 집합을 사용 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="c453a-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="c453a-380">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-380">Element name</span></span>|<span data-ttu-id="c453a-381">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-381">Required</span></span>|<span data-ttu-id="c453a-382">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-382">Type</span></span>|<span data-ttu-id="c453a-383">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="c453a-384">메서드</span><span class="sxs-lookup"><span data-stu-id="c453a-384">method</span></span>|<span data-ttu-id="c453a-385">예</span><span class="sxs-lookup"><span data-stu-id="c453a-385">Yes</span></span>|<span data-ttu-id="c453a-386">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-386">String</span></span>|<span data-ttu-id="c453a-387">Hello HTTP 메서드를 다음 중 하나일 수 있습니다: **가져오기**, **POST**, **배치**, **삭제**, **패치**, 또는  **H E A D**</span><span class="sxs-lookup"><span data-stu-id="c453a-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="c453a-388">uri</span><span class="sxs-lookup"><span data-stu-id="c453a-388">uri</span></span>|<span data-ttu-id="c453a-389">예</span><span class="sxs-lookup"><span data-stu-id="c453a-389">Yes</span></span>|<span data-ttu-id="c453a-390">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-390">String</span></span>|<span data-ttu-id="c453a-391">hello http 또는 https 끝점을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="c453a-392">최대 길이는 2킬로바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="c453a-393">쿼리</span><span class="sxs-lookup"><span data-stu-id="c453a-393">queries</span></span>|<span data-ttu-id="c453a-394">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-394">No</span></span>|<span data-ttu-id="c453a-395">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-395">Object</span></span>|<span data-ttu-id="c453a-396">Hello 쿼리 매개 변수 tooadd toohello URL을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="c453a-397">예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="c453a-398">headers</span><span class="sxs-lookup"><span data-stu-id="c453a-398">headers</span></span>|<span data-ttu-id="c453a-399">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-399">No</span></span>|<span data-ttu-id="c453a-400">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-400">Object</span></span>|<span data-ttu-id="c453a-401">각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="c453a-402">예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="c453a-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="c453a-403">body</span><span class="sxs-lookup"><span data-stu-id="c453a-403">body</span></span>|<span data-ttu-id="c453a-404">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-404">No</span></span>|<span data-ttu-id="c453a-405">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-405">Object</span></span>|<span data-ttu-id="c453a-406">Toohello 끝점으로 전송 되는 hello 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="c453a-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="c453a-407">retryPolicy</span></span>|<span data-ttu-id="c453a-408">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-408">No</span></span>|<span data-ttu-id="c453a-409">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-409">Object</span></span>|<span data-ttu-id="c453a-410">4xx 또는 5xx 오류에 대 한 hello 다시 시도 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="c453a-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="c453a-411">operationsOptions</span></span>|<span data-ttu-id="c453a-412">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-412">No</span></span>|<span data-ttu-id="c453a-413">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-413">String</span></span>|<span data-ttu-id="c453a-414">특별 한 동작 toooverride hello 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="c453a-415">인증</span><span class="sxs-lookup"><span data-stu-id="c453a-415">authentication</span></span>|<span data-ttu-id="c453a-416">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-416">No</span></span>|<span data-ttu-id="c453a-417">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-417">Object</span></span>|<span data-ttu-id="c453a-418">요청 hello 나타냅니다 hello 메서드를 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="c453a-419">이 개체에 대한 자세한 내용은 [스케줄러 아웃바운드 인증](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c453a-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="c453a-420">스케줄러 이외에도 지원되는 속성이 하나 더 있습니다. `authority`</span><span class="sxs-lookup"><span data-stu-id="c453a-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="c453a-421">기본적으로 지정되지 않은 경우 `https://login.windows.net`이지만 `https://login.windows\-ppe.net`과 같이 다른 대상 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="c453a-422">HTTP 작업 \(및 API 연결\) 작업은 다시 시도 정책을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="c453a-423">다시 시도 정책은 toointermittent 오류, HTTP 상태에 대 한 규정 적용 408, 429, 및 추가 tooany 연결 예외가 5xx 코드로 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="c453a-424">이 정책은 hello를 사용 하 여 설명 *retryPolicy* 다음과 같이 정의 된 개체:</span><span class="sxs-lookup"><span data-stu-id="c453a-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="c453a-425">hello 다시 시도 간격 hello ISO 8601 형식으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="c453a-426">Hello 최 댓 값은 1 시간 동안이 간격에 기본값 및 최소값 20 초 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="c453a-427">hello 기본 및 최대 재시도 수는 4 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="c453a-428">Hello 재시도 정책 정의 지정 하지 않은 경우는 `fixed` 전략이 기본 다시 시도 횟수 및 간격 값으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="c453a-429">toodisable hello 재시도 정책을 설정 타입이 너무`None`합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="c453a-430">예를 들어 hello 다음 작업을 다시 시도 반입 hello 최신 뉴스를 두 번 시도 사이의 30 초의 지연 시간에 세 개의 실행 환경에서는 총 일시적인 오류가 발생 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="c453a-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
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
### <a name="asynchronous-patterns"></a><span data-ttu-id="c453a-431">비동기 패턴</span><span class="sxs-lookup"><span data-stu-id="c453a-431">Asynchronous patterns</span></span>

<span data-ttu-id="c453a-432">기본적으로 모든 HTTP 기반 동작 hello 표준 비동기 작업 패턴을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="c453a-433">Hello 원격 서버 hello 요청을 나타내는 경우 202 사용 하 여 처리에 대 한 허용 됩니다 하므로 \("승인 됨"\) 응답으로 hello 논리 앱 엔진 터미널에 도달할 때까지 hello 응답의 위치 헤더에 지정 된 hello URL 폴링 유지 상태 \(비\-202 응답\)합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="c453a-434">이전에 toodisable hello 비동기 동작에서 설명한 설정는 `DisableAsyncPattern` hello 작업 입력에 있는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="c453a-435">이 경우 hello 작업의 출력 hello hello hello 서버에서 초기 202 응답은 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
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

#### <a name="asynchronous-limits"></a><span data-ttu-id="c453a-436">비동기 제한</span><span class="sxs-lookup"><span data-stu-id="c453a-436">Asynchronous Limits</span></span>

<span data-ttu-id="c453a-437">비동기 패턴은 해당 기간 tooa 특정 시간 간격에 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="c453a-438">Hello 동작의 hello 상태 표시될지 터미널 상태에 도달 하지 않고 hello 시간 간격이 지나면 `Cancelled` 코드 `ActionTimedOut`합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="c453a-439">hello 제한 시간 초과 ISO 8601 형식에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="c453a-440">제한 구문 다음 hello로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="c453a-441">API 연결</span><span class="sxs-lookup"><span data-stu-id="c453a-441">API Connection</span></span>  

<span data-ttu-id="c453a-442">API 연결은 Microsoft 관리 커넥터를 참조하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="c453a-443">이 작업에 hello API 및 필요한 매개 변수 방법과 참조 tooa 유효한 연결이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="c453a-444">요소 이름</span><span class="sxs-lookup"><span data-stu-id="c453a-444">Element name</span></span>|<span data-ttu-id="c453a-445">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-445">Required</span></span>|<span data-ttu-id="c453a-446">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-446">Type</span></span>|<span data-ttu-id="c453a-447">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="c453a-448">host</span><span class="sxs-lookup"><span data-stu-id="c453a-448">host</span></span>|<span data-ttu-id="c453a-449">예</span><span class="sxs-lookup"><span data-stu-id="c453a-449">Yes</span></span>|<span data-ttu-id="c453a-450">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-450">Object</span></span>|<span data-ttu-id="c453a-451">Hello runtimeUrl 및 참조 toohello connection 개체와 같은 hello 커넥터 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="c453a-452">메서드</span><span class="sxs-lookup"><span data-stu-id="c453a-452">method</span></span>|<span data-ttu-id="c453a-453">예</span><span class="sxs-lookup"><span data-stu-id="c453a-453">Yes</span></span>|<span data-ttu-id="c453a-454">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-454">String</span></span>|<span data-ttu-id="c453a-455">Hello HTTP 메서드를 다음 중 하나일 수 있습니다: **가져오기**, **POST**, **배치**, **삭제**, **패치**, 또는  **H E A D**</span><span class="sxs-lookup"><span data-stu-id="c453a-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="c453a-456">path</span><span class="sxs-lookup"><span data-stu-id="c453a-456">path</span></span>|<span data-ttu-id="c453a-457">예</span><span class="sxs-lookup"><span data-stu-id="c453a-457">Yes</span></span>|<span data-ttu-id="c453a-458">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-458">String</span></span>|<span data-ttu-id="c453a-459">hello API 작업의 hello 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="c453a-460">쿼리</span><span class="sxs-lookup"><span data-stu-id="c453a-460">queries</span></span>|<span data-ttu-id="c453a-461">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-461">No</span></span>|<span data-ttu-id="c453a-462">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-462">Object</span></span>|<span data-ttu-id="c453a-463">Hello 쿼리 매개 변수 tooadd toohello URL을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="c453a-464">예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="c453a-465">headers</span><span class="sxs-lookup"><span data-stu-id="c453a-465">headers</span></span>|<span data-ttu-id="c453a-466">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-466">No</span></span>|<span data-ttu-id="c453a-467">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-467">Object</span></span>|<span data-ttu-id="c453a-468">각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="c453a-469">예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="c453a-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="c453a-470">body</span><span class="sxs-lookup"><span data-stu-id="c453a-470">body</span></span>|<span data-ttu-id="c453a-471">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-471">No</span></span>|<span data-ttu-id="c453a-472">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-472">Object</span></span>|<span data-ttu-id="c453a-473">Toohello 끝점으로 전송 되는 hello 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="c453a-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="c453a-474">retryPolicy</span></span>|<span data-ttu-id="c453a-475">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-475">No</span></span>|<span data-ttu-id="c453a-476">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-476">Object</span></span>|<span data-ttu-id="c453a-477">4xx 또는 5xx 오류에 대 한 hello 다시 시도 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="c453a-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="c453a-478">operationsOptions</span></span>|<span data-ttu-id="c453a-479">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-479">No</span></span>|<span data-ttu-id="c453a-480">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-480">String</span></span>|<span data-ttu-id="c453a-481">특별 한 동작 toooverride hello 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-481">Defines hello set of special behaviors toooverride.</span></span>|  

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

## <a name="api-connection-webhook-action"></a><span data-ttu-id="c453a-482">API 연결 웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-482">API Connection webhook action</span></span>

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

<span data-ttu-id="c453a-483">Hello webhook 작업에 대 한 제한을 지정할 수와 동일 하 게 [HTTP 비동기 제한](#asynchronous-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="c453a-484">응답 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-484">Response action</span></span>  

<span data-ttu-id="c453a-485">이 동작 형식이 HTTP 요청에서 hello 전체 응답 페이로드를 포함 하 고는 statusCode, 본문 및 헤더를 포함:</span><span class="sxs-lookup"><span data-stu-id="c453a-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
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
  
<span data-ttu-id="c453a-486">hello 응답 동작 tooother 동작이 적용 되지 않는 특별 한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="c453a-487">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-487">Specifically:</span></span>  
  
-   <span data-ttu-id="c453a-488">결정적 응답 toohello 들어오는 요청이 필요 하므로 응답 작업 정의에 병렬 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="c453a-489">Hello 들어오는 요청에 응답을 받은 후 응답 동작에 도달 하면, hello 동작 것으로 간주 됩니다 실패 \(충돌\), 되며 결과적으로, 실행 하는 hello `Failed`합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="c453a-490">응답 작업이 있는 워크플로는 한 번의 호출로 여러 개의 실행이 발생하므로 해당 트리거에 `splitOn`을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="c453a-491">결과적으로,이 유효성을 검사 해야 hello 흐름은 PUT 및 원인은 잘못 된 요청 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c453a-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="c453a-492">대기 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-492">Wait action</span></span>  

<span data-ttu-id="c453a-493">hello `wait` 동작 hello 지정 된 간격에 대 한 워크플로 실행을 일시 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="c453a-494">예를 들어, toowait 15 분이 코드이 조각을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
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
  
<span data-ttu-id="c453a-495">또는 toowait를 특정 시점에에서 될 때까지이 예제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
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
> <span data-ttu-id="c453a-496">hello 대기 시간이 하거나 지정할 수 hello를 사용 하 여 **간격** 개체나 hello **될 때까지** 개체가 아니라 둘 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="c453a-497">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-497">Name</span></span>|<span data-ttu-id="c453a-498">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-498">Required</span></span>|<span data-ttu-id="c453a-499">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-499">Type</span></span>|<span data-ttu-id="c453a-500">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="c453a-501">interval</span><span class="sxs-lookup"><span data-stu-id="c453a-501">interval</span></span>|<span data-ttu-id="c453a-502">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-502">No</span></span>|<span data-ttu-id="c453a-503">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-503">Object</span></span>|<span data-ttu-id="c453a-504">hello 대기 시간에 따라 기간.</span><span class="sxs-lookup"><span data-stu-id="c453a-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="c453a-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="c453a-505">interval unit</span></span>|<span data-ttu-id="c453a-506">예</span><span class="sxs-lookup"><span data-stu-id="c453a-506">Yes</span></span>|<span data-ttu-id="c453a-507">String</span><span class="sxs-lookup"><span data-stu-id="c453a-507">String</span></span>|<span data-ttu-id="c453a-508">second, minute, hour, day, week, month, year 간격 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="c453a-509">interval count</span><span class="sxs-lookup"><span data-stu-id="c453a-509">interval count</span></span>|<span data-ttu-id="c453a-510">예</span><span class="sxs-lookup"><span data-stu-id="c453a-510">Yes</span></span>|<span data-ttu-id="c453a-511">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-511">String</span></span>|<span data-ttu-id="c453a-512">내부 단위를 지정 하는 hello에 따라 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="c453a-513">until</span><span class="sxs-lookup"><span data-stu-id="c453a-513">until</span></span>|<span data-ttu-id="c453a-514">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-514">No</span></span>|<span data-ttu-id="c453a-515">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-515">Object</span></span>|<span data-ttu-id="c453a-516">hello 대기 시간에는 지점에 기반 하는 기간.</span><span class="sxs-lookup"><span data-stu-id="c453a-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="c453a-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="c453a-517">until timestamp</span></span>|<span data-ttu-id="c453a-518">예</span><span class="sxs-lookup"><span data-stu-id="c453a-518">Yes</span></span>|<span data-ttu-id="c453a-519">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-519">String</span></span>|<span data-ttu-id="c453a-520">문자열 &#124; hello 지정 hello 대기 만료 될 때 utc에서 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="c453a-521">쿼리 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-521">Query action</span></span>

<span data-ttu-id="c453a-522">hello `query` 작업을 사용 하면 조건에 따라 배열을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="c453a-523">예를 들어 tooselect 2 보다 큰 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="c453a-524">hello 출력 hello `query` 동작은 hello 조건을 만족 하는 hello 입력 배열에서 요소가 포함 된 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="c453a-525">Hello를 만족 하는 값이 없는 경우 `where` 조건의 경우 hello 결과 빈 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="c453a-526">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-526">Name</span></span>|<span data-ttu-id="c453a-527">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-527">Required</span></span>|<span data-ttu-id="c453a-528">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-528">Type</span></span>|<span data-ttu-id="c453a-529">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="c453a-530">from</span><span class="sxs-lookup"><span data-stu-id="c453a-530">from</span></span>|<span data-ttu-id="c453a-531">예</span><span class="sxs-lookup"><span data-stu-id="c453a-531">Yes</span></span>|<span data-ttu-id="c453a-532">배열</span><span class="sxs-lookup"><span data-stu-id="c453a-532">Array</span></span>|<span data-ttu-id="c453a-533">hello 소스 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-533">hello source array.</span></span>|
|<span data-ttu-id="c453a-534">여기서,</span><span class="sxs-lookup"><span data-stu-id="c453a-534">where</span></span>|<span data-ttu-id="c453a-535">예</span><span class="sxs-lookup"><span data-stu-id="c453a-535">Yes</span></span>|<span data-ttu-id="c453a-536">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-536">String</span></span>|<span data-ttu-id="c453a-537">hello 조건 tooapply tooeach hello 소스 배열의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="c453a-538">작업 선택</span><span class="sxs-lookup"><span data-stu-id="c453a-538">Select action</span></span>

<span data-ttu-id="c453a-539">hello `select` 작업을 사용 하면 새 값으로는 배열의 각 요소를 프로젝션 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="c453a-540">예를 들어, 개체의 배열에는 숫자의 배열을 tooconvert 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="c453a-541">출력의 hello hello `select` 동작은 hello 하 여 hello 동일한 카디널리티 변환 된 각 요소와 입력된 배열의 hello으로 정의 된 배열을 `select` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="c453a-542">빈 배열을 hello 입력을 사용 하는 경우 hello 출력 빈 배열을 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="c453a-543">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-543">Name</span></span>|<span data-ttu-id="c453a-544">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-544">Required</span></span>|<span data-ttu-id="c453a-545">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-545">Type</span></span>|<span data-ttu-id="c453a-546">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="c453a-547">from</span><span class="sxs-lookup"><span data-stu-id="c453a-547">from</span></span>|<span data-ttu-id="c453a-548">예</span><span class="sxs-lookup"><span data-stu-id="c453a-548">Yes</span></span>|<span data-ttu-id="c453a-549">배열</span><span class="sxs-lookup"><span data-stu-id="c453a-549">Array</span></span>|<span data-ttu-id="c453a-550">hello 소스 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-550">hello source array.</span></span>|
|<span data-ttu-id="c453a-551">선택</span><span class="sxs-lookup"><span data-stu-id="c453a-551">select</span></span>|<span data-ttu-id="c453a-552">예</span><span class="sxs-lookup"><span data-stu-id="c453a-552">Yes</span></span>|<span data-ttu-id="c453a-553">모두</span><span class="sxs-lookup"><span data-stu-id="c453a-553">Any</span></span>|<span data-ttu-id="c453a-554">hello 프로젝션 tooapply tooeach hello 소스 배열의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="c453a-555">종료 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-555">Terminate action</span></span>

<span data-ttu-id="c453a-556">hello 종결 동작 hello 워크플로 실행을 모든 진행 중인 작업을 중단 하 고 남은 작업도 건너뜁니다의 실행을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="c453a-557">Tooterminate 상태와 함께 실행 하는 예를 들어 **실패**, 다음 코드 조각 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

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
> <span data-ttu-id="c453a-558">작업을 이미 완료 hello 영향을 받지 않는 작업을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="c453a-559">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-559">Name</span></span>|<span data-ttu-id="c453a-560">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-560">Required</span></span>|<span data-ttu-id="c453a-561">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-561">Type</span></span>|<span data-ttu-id="c453a-562">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="c453a-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="c453a-563">runStatus</span></span>|<span data-ttu-id="c453a-564">예</span><span class="sxs-lookup"><span data-stu-id="c453a-564">Yes</span></span>|<span data-ttu-id="c453a-565">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-565">String</span></span>|<span data-ttu-id="c453a-566">hello 대상 실행 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-566">hello target run status.</span></span> <span data-ttu-id="c453a-567">**Failed** 또는 **Cancelled**입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="c453a-568">runError</span><span class="sxs-lookup"><span data-stu-id="c453a-568">runError</span></span>|<span data-ttu-id="c453a-569">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-569">No</span></span>|<span data-ttu-id="c453a-570">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-570">Object</span></span>|<span data-ttu-id="c453a-571">hello 오류 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-571">hello error details.</span></span> <span data-ttu-id="c453a-572">실행할 수만 **runStatus** 너무 설정**실패**합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="c453a-573">runError code</span><span class="sxs-lookup"><span data-stu-id="c453a-573">runError code</span></span>|<span data-ttu-id="c453a-574">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-574">No</span></span>|<span data-ttu-id="c453a-575">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-575">String</span></span>|<span data-ttu-id="c453a-576">오류 코드를 실행 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-576">hello run error code.</span></span>|
|<span data-ttu-id="c453a-577">runError message</span><span class="sxs-lookup"><span data-stu-id="c453a-577">runError message</span></span>|<span data-ttu-id="c453a-578">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-578">No</span></span>|<span data-ttu-id="c453a-579">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-579">String</span></span>|<span data-ttu-id="c453a-580">오류 메시지를 실행 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="c453a-581">작성 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-581">Compose action</span></span>

<span data-ttu-id="c453a-582">hello 작성 작업을 사용 하면 임의의 개체를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="c453a-583">hello의 hello 출력 작성 작업은 해당 입력 평가 hello 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="c453a-584">예를 들어 hello를 사용할 수 있습니다 여러 동작의 작업 toomerge 출력을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

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
> <span data-ttu-id="c453a-585">hello **Compose** 동작 개체, 배열 및 기본적으로 XML 및 이진 같은 논리 앱에서 지 원하는 다른 형식을 포함 하 여 출력을 사용 하는 tooconstruct를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="c453a-586">테이블 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-586">Table action</span></span>

<span data-ttu-id="c453a-587">hello `table` tooconvert에 항목 배열을 사용 하면 한 **CSV** 또는 **HTML** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="c453a-588">@triggerBody()을 다음으로 가정합니다</span><span class="sxs-lookup"><span data-stu-id="c453a-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="c453a-589">Hello 동작으로 정의할 수 있도록</span><span class="sxs-lookup"><span data-stu-id="c453a-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="c453a-590">위의 hello 생성</span><span class="sxs-lookup"><span data-stu-id="c453a-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="c453a-591">id</span><span class="sxs-lookup"><span data-stu-id="c453a-591">id</span></span></th><th><span data-ttu-id="c453a-592">name</span><span class="sxs-lookup"><span data-stu-id="c453a-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="c453a-593">0</span><span class="sxs-lookup"><span data-stu-id="c453a-593">0</span></span></td><td><span data-ttu-id="c453a-594">사과</span><span class="sxs-lookup"><span data-stu-id="c453a-594">apples</span></span></td></tr><tr><td><span data-ttu-id="c453a-595">1</span><span class="sxs-lookup"><span data-stu-id="c453a-595">1</span></span></td><td><span data-ttu-id="c453a-596">오렌지</span><span class="sxs-lookup"><span data-stu-id="c453a-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="c453a-597">"</span><span class="sxs-lookup"><span data-stu-id="c453a-597">"</span></span>

<span data-ttu-id="c453a-598">순서 toocustomize hello 표에 hello 열을 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="c453a-599">예:</span><span class="sxs-lookup"><span data-stu-id="c453a-599">For example:</span></span>

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

<span data-ttu-id="c453a-600">위의 hello 생성</span><span class="sxs-lookup"><span data-stu-id="c453a-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="c453a-601">ID를 생성합니다</span><span class="sxs-lookup"><span data-stu-id="c453a-601">produce id</span></span></th><th><span data-ttu-id="c453a-602">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="c453a-603">0</span><span class="sxs-lookup"><span data-stu-id="c453a-603">0</span></span></td><td><span data-ttu-id="c453a-604">신선한 사과</span><span class="sxs-lookup"><span data-stu-id="c453a-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="c453a-605">1</span><span class="sxs-lookup"><span data-stu-id="c453a-605">1</span></span></td><td><span data-ttu-id="c453a-606">신선한 오렌지</span><span class="sxs-lookup"><span data-stu-id="c453a-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="c453a-607">"</span><span class="sxs-lookup"><span data-stu-id="c453a-607">"</span></span>

<span data-ttu-id="c453a-608">경우 hello `from` hello 출력은 빈 테이블, 속성 값은 빈 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="c453a-609">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-609">Name</span></span>|<span data-ttu-id="c453a-610">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-610">Required</span></span>|<span data-ttu-id="c453a-611">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-611">Type</span></span>|<span data-ttu-id="c453a-612">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="c453a-613">from</span><span class="sxs-lookup"><span data-stu-id="c453a-613">from</span></span>|<span data-ttu-id="c453a-614">예</span><span class="sxs-lookup"><span data-stu-id="c453a-614">Yes</span></span>|<span data-ttu-id="c453a-615">배열</span><span class="sxs-lookup"><span data-stu-id="c453a-615">Array</span></span>|<span data-ttu-id="c453a-616">hello 소스 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-616">hello source array.</span></span>|
|<span data-ttu-id="c453a-617">format</span><span class="sxs-lookup"><span data-stu-id="c453a-617">format</span></span>|<span data-ttu-id="c453a-618">예</span><span class="sxs-lookup"><span data-stu-id="c453a-618">Yes</span></span>|<span data-ttu-id="c453a-619">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-619">String</span></span>|<span data-ttu-id="c453a-620">형식으로 하거나 hello **CSV** 또는 **HTML**합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="c453a-621">열</span><span class="sxs-lookup"><span data-stu-id="c453a-621">columns</span></span>|<span data-ttu-id="c453a-622">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-622">No</span></span>|<span data-ttu-id="c453a-623">배열</span><span class="sxs-lookup"><span data-stu-id="c453a-623">Array</span></span>|<span data-ttu-id="c453a-624">hello 열입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-624">hello columns.</span></span> <span data-ttu-id="c453a-625">Hello 표의 toooverride hello 기본 형태를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="c453a-626">열 머리글</span><span class="sxs-lookup"><span data-stu-id="c453a-626">column header</span></span>|<span data-ttu-id="c453a-627">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-627">No</span></span>|<span data-ttu-id="c453a-628">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-628">String</span></span>|<span data-ttu-id="c453a-629">hello 열의 hello 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-629">hello header of hello column.</span></span>|
|<span data-ttu-id="c453a-630">열 값</span><span class="sxs-lookup"><span data-stu-id="c453a-630">column value</span></span>|<span data-ttu-id="c453a-631">예</span><span class="sxs-lookup"><span data-stu-id="c453a-631">Yes</span></span>|<span data-ttu-id="c453a-632">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-632">String</span></span>|<span data-ttu-id="c453a-633">hello 열의 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="c453a-634">워크플로 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-634">Workflow action</span></span>   

|<span data-ttu-id="c453a-635">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-635">Name</span></span>|<span data-ttu-id="c453a-636">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-636">Required</span></span>|<span data-ttu-id="c453a-637">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-637">Type</span></span>|<span data-ttu-id="c453a-638">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="c453a-639">host id</span><span class="sxs-lookup"><span data-stu-id="c453a-639">host id</span></span>|<span data-ttu-id="c453a-640">예</span><span class="sxs-lookup"><span data-stu-id="c453a-640">Yes</span></span>|<span data-ttu-id="c453a-641">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-641">String</span></span>|<span data-ttu-id="c453a-642">hello toocall hello 워크플로의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="c453a-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="c453a-643">host triggerName</span></span>|<span data-ttu-id="c453a-644">예</span><span class="sxs-lookup"><span data-stu-id="c453a-644">Yes</span></span>|<span data-ttu-id="c453a-645">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-645">String</span></span>|<span data-ttu-id="c453a-646">tooinvoke hello 트리거가의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="c453a-647">쿼리</span><span class="sxs-lookup"><span data-stu-id="c453a-647">queries</span></span>|<span data-ttu-id="c453a-648">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-648">No</span></span>|<span data-ttu-id="c453a-649">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-649">Object</span></span>|<span data-ttu-id="c453a-650">Hello 쿼리 매개 변수 tooadd toohello URL을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="c453a-651">예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="c453a-652">headers</span><span class="sxs-lookup"><span data-stu-id="c453a-652">headers</span></span>|<span data-ttu-id="c453a-653">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-653">No</span></span>|<span data-ttu-id="c453a-654">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-654">Object</span></span>|<span data-ttu-id="c453a-655">각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="c453a-656">예를 들어 tooset hello 언어 및 요청에는 형식:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="c453a-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="c453a-657">body</span><span class="sxs-lookup"><span data-stu-id="c453a-657">body</span></span>|<span data-ttu-id="c453a-658">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-658">No</span></span>|<span data-ttu-id="c453a-659">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-659">Object</span></span>|<span data-ttu-id="c453a-660">Toohello 끝점으로 전송 하는 hello 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
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
  
<span data-ttu-id="c453a-661">액세스 검사 hello 워크플로에서 만든 \(hello 트리거 보다 구체적으로,\), toohello 워크플로 액세스 할 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="c453a-662">hello hello에서 출력 `workflow` hello에 정의 된에 기반한 동작 `response` hello 자식 워크플로에서 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="c453a-663">정의 되지 않은 경우 `response` 작업과 차례로 hello 출력 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="c453a-664">Function 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-664">Function action</span></span>   

|<span data-ttu-id="c453a-665">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-665">Name</span></span>|<span data-ttu-id="c453a-666">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-666">Required</span></span>|<span data-ttu-id="c453a-667">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-667">Type</span></span>|<span data-ttu-id="c453a-668">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="c453a-669">function id</span><span class="sxs-lookup"><span data-stu-id="c453a-669">function id</span></span>|<span data-ttu-id="c453a-670">예</span><span class="sxs-lookup"><span data-stu-id="c453a-670">Yes</span></span>|<span data-ttu-id="c453a-671">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-671">String</span></span>|<span data-ttu-id="c453a-672">hello tooinvoke hello 함수의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="c453a-673">메서드</span><span class="sxs-lookup"><span data-stu-id="c453a-673">method</span></span>|<span data-ttu-id="c453a-674">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-674">No</span></span>|<span data-ttu-id="c453a-675">문자열</span><span class="sxs-lookup"><span data-stu-id="c453a-675">String</span></span>|<span data-ttu-id="c453a-676">HTTP 메서드 hello tooinvoke hello 함수를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="c453a-677">기본적으로 지정되지 않은 경우 `POST`입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="c453a-678">쿼리</span><span class="sxs-lookup"><span data-stu-id="c453a-678">queries</span></span>|<span data-ttu-id="c453a-679">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-679">No</span></span>|<span data-ttu-id="c453a-680">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-680">Object</span></span>|<span data-ttu-id="c453a-681">Hello 쿼리 매개 변수 tooadd toohello URL을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="c453a-682">예를 들어 `"queries" : { "api-version": "2015-02-01" }` 추가 `?api-version=2015-02-01` toohello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="c453a-683">headers</span><span class="sxs-lookup"><span data-stu-id="c453a-683">headers</span></span>|<span data-ttu-id="c453a-684">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-684">No</span></span>|<span data-ttu-id="c453a-685">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-685">Object</span></span>|<span data-ttu-id="c453a-686">각각의 toohello 요청이 발송 되 hello 머리글을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="c453a-687">예를 들어: tooset hello 언어와 요청에는 유형을: `"headers" : { "Accept-Language": "en-us" }`합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="c453a-688">body</span><span class="sxs-lookup"><span data-stu-id="c453a-688">body</span></span>|<span data-ttu-id="c453a-689">아니요</span><span class="sxs-lookup"><span data-stu-id="c453a-689">No</span></span>|<span data-ttu-id="c453a-690">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-690">Object</span></span>|<span data-ttu-id="c453a-691">Toohello 끝점으로 전송 하는 hello 페이로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-691">Represents hello payload sent toohello endpoint.</span></span>|  

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

<span data-ttu-id="c453a-692">Hello 논리 앱을 저장할 때 참조 된 hello 함수에 대 한 몇 가지 검사 수행:</span><span class="sxs-lookup"><span data-stu-id="c453a-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="c453a-693">Toohave access toohello 함수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="c453a-694">표준 HTTP 트리거 또는 일반 JSON 웹후크 트리거만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="c453a-695">경로를 정의하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="c453a-696">"함수" 및 "익명" 권한 부여 수준만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="c453a-697">hello 트리거 URL 검색, 캐시 및 런타임에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="c453a-698">따라서 캐시 hello URL을 무효화 하는 모든 작업을 런타임 시 hello 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="c453a-699">이 문제를 해결 toowork hello 논리 다시 응용 프로그램, 논리 앱 tooretrieve 되며 hello 트리거 URL을 다시 캐시를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="c453a-700">컬렉션 작업(범위 및 루프)</span><span class="sxs-lookup"><span data-stu-id="c453a-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="c453a-701">일부 작업 유형은 자체 내에 작업을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="c453a-702">컬렉션 내에서 동작 참조 hello 컬렉션 외부에서 직접 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="c453a-703">범위에 `http`를 정의한 경우 `@body('http')`는 워크플로 어느 곳에서나 여전히 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="c453a-704">컬렉션 내에서 동작의 기능은 `runAfter` 내에서 다른 작업에만 hello 동일한 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="c453a-705">범위 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-705">Scope action</span></span>

<span data-ttu-id="c453a-706">hello `scope` 동작을 수행 하면 논리적으로 워크플로에서 그룹 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="c453a-707">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-707">Name</span></span>|<span data-ttu-id="c453a-708">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-708">Required</span></span>|<span data-ttu-id="c453a-709">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-709">Type</span></span>|<span data-ttu-id="c453a-710">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="c453a-711">actions</span><span class="sxs-lookup"><span data-stu-id="c453a-711">actions</span></span>|<span data-ttu-id="c453a-712">예</span><span class="sxs-lookup"><span data-stu-id="c453a-712">Yes</span></span>|<span data-ttu-id="c453a-713">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-713">Object</span></span>|<span data-ttu-id="c453a-714">내부 작업 tooexecute hello 범위 내에서</span><span class="sxs-lookup"><span data-stu-id="c453a-714">Inner actions tooexecute within hello scope</span></span>|

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

## <a name="foreach-action"></a><span data-ttu-id="c453a-715">ForEach 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-715">ForEach action</span></span>

<span data-ttu-id="c453a-716">이 루프 작업은 배열을 반복하고 각 항목에 대해 내부 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="c453a-717">기본적으로 hello foreach 루프 (20 번 실행 동시에 한 번에) 병렬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="c453a-718">Hello를 사용 하 여 실행 규칙을 설정할 수 있습니다 `operationOptions` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="c453a-719">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-719">Name</span></span>|<span data-ttu-id="c453a-720">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-720">Required</span></span>|<span data-ttu-id="c453a-721">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-721">Type</span></span>|<span data-ttu-id="c453a-722">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="c453a-723">actions</span><span class="sxs-lookup"><span data-stu-id="c453a-723">actions</span></span>|<span data-ttu-id="c453a-724">예</span><span class="sxs-lookup"><span data-stu-id="c453a-724">Yes</span></span>|<span data-ttu-id="c453a-725">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-725">Object</span></span>|<span data-ttu-id="c453a-726">내부 작업 tooexecute hello 루프 내에서</span><span class="sxs-lookup"><span data-stu-id="c453a-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="c453a-727">foreach</span><span class="sxs-lookup"><span data-stu-id="c453a-727">foreach</span></span>|<span data-ttu-id="c453a-728">예</span><span class="sxs-lookup"><span data-stu-id="c453a-728">Yes</span></span>|<span data-ttu-id="c453a-729">string</span><span class="sxs-lookup"><span data-stu-id="c453a-729">string</span></span>|<span data-ttu-id="c453a-730">통해 배열 tooiterate hello</span><span class="sxs-lookup"><span data-stu-id="c453a-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="c453a-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="c453a-731">operationOptions</span></span>|<span data-ttu-id="c453a-732">no</span><span class="sxs-lookup"><span data-stu-id="c453a-732">no</span></span>|<span data-ttu-id="c453a-733">string</span><span class="sxs-lookup"><span data-stu-id="c453a-733">string</span></span>|<span data-ttu-id="c453a-734">동작에 대한 모든 작업 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-734">Any operation options for behavior.</span></span> <span data-ttu-id="c453a-735">현재 까지만 지원 `sequential` tooexecute 반복 순서 대로) (기본 동작은 병렬)</span><span class="sxs-lookup"><span data-stu-id="c453a-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

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

## <a name="until-action"></a><span data-ttu-id="c453a-736">Until 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-736">Until action</span></span>

<span data-ttu-id="c453a-737">이 반복 작업 조건 결과 tootrue 될 때까지 내부 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="c453a-738">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-738">Name</span></span>|<span data-ttu-id="c453a-739">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-739">Required</span></span>|<span data-ttu-id="c453a-740">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-740">Type</span></span>|<span data-ttu-id="c453a-741">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="c453a-742">actions</span><span class="sxs-lookup"><span data-stu-id="c453a-742">actions</span></span>|<span data-ttu-id="c453a-743">예</span><span class="sxs-lookup"><span data-stu-id="c453a-743">Yes</span></span>|<span data-ttu-id="c453a-744">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-744">Object</span></span>|<span data-ttu-id="c453a-745">내부 작업 tooexecute hello 루프 내에서</span><span class="sxs-lookup"><span data-stu-id="c453a-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="c453a-746">식</span><span class="sxs-lookup"><span data-stu-id="c453a-746">expression</span></span>|<span data-ttu-id="c453a-747">예</span><span class="sxs-lookup"><span data-stu-id="c453a-747">Yes</span></span>|<span data-ttu-id="c453a-748">string</span><span class="sxs-lookup"><span data-stu-id="c453a-748">string</span></span>|<span data-ttu-id="c453a-749">반복할 때마다 식 tooevaluate hello</span><span class="sxs-lookup"><span data-stu-id="c453a-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="c453a-750">limit</span><span class="sxs-lookup"><span data-stu-id="c453a-750">limit</span></span>|<span data-ttu-id="c453a-751">yes</span><span class="sxs-lookup"><span data-stu-id="c453a-751">yes</span></span>|<span data-ttu-id="c453a-752">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-752">Object</span></span>|<span data-ttu-id="c453a-753">hello 반복-하나 이상의 제한에 대 한 hello도 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="c453a-754">count</span><span class="sxs-lookup"><span data-stu-id="c453a-754">count</span></span>|<span data-ttu-id="c453a-755">no</span><span class="sxs-lookup"><span data-stu-id="c453a-755">no</span></span>|<span data-ttu-id="c453a-756">int</span><span class="sxs-lookup"><span data-stu-id="c453a-756">int</span></span>|<span data-ttu-id="c453a-757">수행할 수 있는 반복 횟수 제한 toohello hello</span><span class="sxs-lookup"><span data-stu-id="c453a-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="c453a-758">시간 제한</span><span class="sxs-lookup"><span data-stu-id="c453a-758">timeout</span></span>|<span data-ttu-id="c453a-759">no</span><span class="sxs-lookup"><span data-stu-id="c453a-759">no</span></span>|<span data-ttu-id="c453a-760">string</span><span class="sxs-lookup"><span data-stu-id="c453a-760">string</span></span>|<span data-ttu-id="c453a-761">반복 기간에 대 한 hello 시간이 초과 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="c453a-762">ISO 8601 형식</span><span class="sxs-lookup"><span data-stu-id="c453a-762">ISO 8601 format</span></span>|


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

## <a name="conditions---if-action"></a><span data-ttu-id="c453a-763">조건 - If 작업</span><span class="sxs-lookup"><span data-stu-id="c453a-763">Conditions - If Action</span></span>

<span data-ttu-id="c453a-764">hello `If` 조건을 평가 하 고 hello 식이 너무 계산 여부에 따라 분기 실행 동작을 수행 하면`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="c453a-765">이름</span><span class="sxs-lookup"><span data-stu-id="c453a-765">Name</span></span>|<span data-ttu-id="c453a-766">필수</span><span class="sxs-lookup"><span data-stu-id="c453a-766">Required</span></span>|<span data-ttu-id="c453a-767">형식</span><span class="sxs-lookup"><span data-stu-id="c453a-767">Type</span></span>|<span data-ttu-id="c453a-768">설명</span><span class="sxs-lookup"><span data-stu-id="c453a-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="c453a-769">actions</span><span class="sxs-lookup"><span data-stu-id="c453a-769">actions</span></span>|<span data-ttu-id="c453a-770">예</span><span class="sxs-lookup"><span data-stu-id="c453a-770">Yes</span></span>|<span data-ttu-id="c453a-771">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-771">Object</span></span>|<span data-ttu-id="c453a-772">내부 작업 tooexecute 식이 너무 평가 되 면`true`</span><span class="sxs-lookup"><span data-stu-id="c453a-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="c453a-773">식</span><span class="sxs-lookup"><span data-stu-id="c453a-773">expression</span></span>|<span data-ttu-id="c453a-774">예</span><span class="sxs-lookup"><span data-stu-id="c453a-774">Yes</span></span>|<span data-ttu-id="c453a-775">string</span><span class="sxs-lookup"><span data-stu-id="c453a-775">string</span></span>|<span data-ttu-id="c453a-776">hello 식 tooevaluate</span><span class="sxs-lookup"><span data-stu-id="c453a-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="c453a-777">else</span><span class="sxs-lookup"><span data-stu-id="c453a-777">else</span></span>|<span data-ttu-id="c453a-778">no</span><span class="sxs-lookup"><span data-stu-id="c453a-778">no</span></span>|<span data-ttu-id="c453a-779">Object</span><span class="sxs-lookup"><span data-stu-id="c453a-779">Object</span></span>|<span data-ttu-id="c453a-780">내부 작업 tooexecute 식이 너무 평가 되 면`false`</span><span class="sxs-lookup"><span data-stu-id="c453a-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
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
  
<span data-ttu-id="c453a-781">hello 다음 표에서 사용 방법의 조건 식 동작:</span><span class="sxs-lookup"><span data-stu-id="c453a-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="c453a-782">JSON 값</span><span class="sxs-lookup"><span data-stu-id="c453a-782">JSON value</span></span>|<span data-ttu-id="c453a-783">결과</span><span class="sxs-lookup"><span data-stu-id="c453a-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="c453a-784">Tootrue를 평가 하는 모든 값이 조건 toopass를 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="c453a-785">부울 식만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="c453a-786">다른 tooconvert tooBoolean를 사용 하 여 함수 형식 `empty`, `equals`합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="c453a-787">비교 함수는 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-787">Comparison functions are supported.</span></span> <span data-ttu-id="c453a-788">예: hello 여기 hello 동작 act1의 hello 출력 hello 임계값 보다 큰 경우에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="c453a-789">논리 함수는 또한 지원 되는 toocreate 중첩 부울 식입니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="c453a-790">이 경우 hello 동작 act1 hello 출력은 100 이하일 hello 임계값을 초과 하는 경우를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="c453a-791">배열에 항목이 있으면 배열 함수 toocheck를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="c453a-792">이 경우 hello 동작 hello 오류 배열이 비어 있는 경우를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="c453a-793">오류 - 조건에 @이 필요하므로 유효한 조건이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="c453a-794">Hello 조건으로 표시 되어 조건이 성공적으로 확인 되 면 `Succeeded`합니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="c453a-795">어느 hello 내의 동작 `actions` 또는 `else` 개체 너무 평가`Succeeded` 실행 한 성공한 경우 `Failed` 실행 한 실패 한 경우 또는 `Skipped` 해당 분기는 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c453a-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c453a-796">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c453a-796">Next steps</span></span>

[<span data-ttu-id="c453a-797">워크플로 서비스 REST API</span><span class="sxs-lookup"><span data-stu-id="c453a-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
