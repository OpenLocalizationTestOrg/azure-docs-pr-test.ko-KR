---
title: "aaaError & 예외 처리-Azure 논리 앱 | Microsoft Docs"
description: "Azure Logic Apps에서 오류 및 예외 처리 패턴"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="b4c74-103">Azure Logic Apps에서 예외 및 오류 처리</span><span class="sxs-lookup"><span data-stu-id="b4c74-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="b4c74-104">패턴 toohelp 수 있도록 사용자 통합은 강력 하 고 오류에 대 한 복원 력이 및 azure 논리 앱 풍부한 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="b4c74-105">모든 통합 아키텍처 있는지 tooappropriately 핸들 가동 중지 시간 삼기 hello challenge로 인해 발생 하며 또는 종속 시스템의 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="b4c74-106">오류 처리 논리 앱 사용 하면 제공 하는 첫 번째 클래스 환경을 hello 워크플로에서 tooact 예외 및 오류에 필요한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="b4c74-107">재시도 정책</span><span class="sxs-lookup"><span data-stu-id="b4c74-107">Retry policies</span></span>

<span data-ttu-id="b4c74-108">다시 시도 정책은 hello 예외 및 오류 처리의 가장 기본적인 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="b4c74-109">초기 요청 시간 초과 또는 실패 한 경우 (429는 발생 하는 모든 요청 또는 5xx 응답),이 정책은 hello 작업을 다시 시도해 야 하는지 여부를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="b4c74-110">기본적으로 모든 작업은 20초 간격에 걸쳐 추가로 4회 재시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="b4c74-111">따라서 hello 첫 번째 요청 수신 하는 경우는 `500 Internal Server Error` 시도 안녕 요청 및 응답으로 hello 워크플로 엔진 20 초 동안 일시 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="b4c74-112">Hello 워크플로에서 계속 하는 경우 모든 다시 시도한 후 hello 응답은 여전히 예외 또는 오류, 및 표시로 작업 상태를 hello `Failed`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="b4c74-113">Hello에 다시 시도 정책을 구성할 수 있습니다 **입력** 특정 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="b4c74-114">예를 들어 구성할 수 있습니다 다시 시도 정책 tootry 4 회까지 1 시간 간격에 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="b4c74-115">입력 속성에 대한 자세한 내용은 [워크플로 작업 및 트리거][retryPolicyMSDN]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c74-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="b4c74-116">HTTP 동작 tooretry 4 번 려 하 고 각 시도 사이 10 분 정도 기다린 다음 정의 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="b4c74-117">지원 되는 구문에 대 한 자세한 내용은 참조 hello [워크플로 동작 및 트리거에 다시 시도 정책 섹션][retryPolicyMSDN]합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="b4c74-118">Hello RunAfter 속성으로 오류를 catch 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="b4c74-119">각 논리 앱 작업 선언 워크플로에 hello 단계 순서와 같은 hello 작업이 시작 되기 전에 작업을 마쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="b4c74-120">Hello 작업 정의에이 순서 라고 hello `runAfter` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="b4c74-121">이 속성은 hello 작업을 실행 하는 작업 및 작업 상태를 설명 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="b4c74-122">기본적으로 hello 논리가 응용 프로그램 디자이너를 통해 추가 된 모든 작업은 설정 너무`runAfter` hello 이전 단계 경우 hello 이전 단계 `Succeeded`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="b4c74-123">그러나 이전 작업 해야 하는 경우이 값 toofire 동작을 사용자 지정할 수 `Failed`, `Skipped`, 또는 이러한 값의 가능한 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="b4c74-124">특정 작업 후 항목 tooa 서비스 버스 항목 지정 tooadd 려 `Insert_Row` 실패 하면 다음 hello를 사용할 수 있습니다 `runAfter` 구성:</span><span class="sxs-lookup"><span data-stu-id="b4c74-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="b4c74-125">공지 hello `runAfter` 속성이 toofire 경우 hello `Insert_Row` 동작은 `Failed`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="b4c74-126">toorun hello 동작 hello 작업 상태 이면 `Succeeded`, `Failed`, 또는 `Skipped`,이 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="b4c74-127">이전 작업이 실패한 후 실행되는 작업이 성공적으로 완료되면 `Succeeded`로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="b4c74-128">이 동작은 실행을 의미 hello 하면 워크플로에서 성공적으로 모든 catch 실패 하는 경우 자체로 표시 되어 `Succeeded`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="b4c74-129">범위 및 결과 tooevaluate 작업</span><span class="sxs-lookup"><span data-stu-id="b4c74-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="b4c74-130">비슷한 toohow 개별 작업 후에 실행할 수, 또한 함께 그룹화 할 수 작업 내는 [범위](../logic-apps/logic-apps-loops-and-scopes.md), 작업의 논리적 그룹으로 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="b4c74-131">범위는 범위의 hello 상태에서 집계 평가 수행 하기 위한 및 논리 앱 작업을 구성 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="b4c74-132">자체 hello 범위는 범위에서 작업을 모두 완료 한 후 상태를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="b4c74-133">hello 범위 상태는 hello로 결정 됩니다. 동일한 기준으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="b4c74-134">실행 분기의 마지막 작업에서는 hello 경우 `Failed` 또는 `Aborted`, hello 상태는 `Failed`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="b4c74-135">사용할 수 있습니다 toofire hello 범위 내에서 수행 된 모든 오류에 대 한 특정 작업을 `runAfter` 표시 된 범위를 갖는 `Failed`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="b4c74-136">경우 *모든* hello 범위에는 동작이 실패 하는 경우 범위를 사용 하면 실패 한 후에 실행 되도록 만들 단일 작업 toocatch 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="b4c74-137">결과와 관련 된 오류 컨텍스트 hello 가져오기</span><span class="sxs-lookup"><span data-stu-id="b4c74-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="b4c74-138">범위에서 오류를 catch 하는 것은 유용, 있지만 컨텍스트 toohelp 실패 하는 작업을 정확 하 게 이해 하 고 오류 또는 반환 된 상태 코드도 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="b4c74-139">hello `@result()` 워크플로 함수는 범위에 있는 모든 작업의 결과 hello에 대 한 컨텍스트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="b4c74-140">`@result()`단일 매개 변수, 범위 이름 하며 해당 범위 내에서 모든 hello 작업 결과의 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="b4c74-141">이러한 작업 개체에 hello로 특성 동일 hello 포함 `@actions()` 작업 시작 시간, 작업 종료 시간, 작업 상태, 작업 입력, 작업 상관관계 Id 및 동작을 포함 하 여 개체를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="b4c74-142">범위 내에서 실패 한 작업 toosend 컨텍스트를 쉽게 연결할 수는 `@result()` 작동 한 `runAfter`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="b4c74-143">tooexecute 동작 *각* 범위에서 동작 하는 `Failed`, 필터 hello 배열을 결과 tooactions 배포 하지 못한, 페어링할 수 있는 `@result()` 와  **[필터 배열](../connectors/connectors-native-query.md)**  동작 및  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  루프입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="b4c74-144">Hello 필터링 된 결과 배열 고 hello를 사용 하 여 각 오류에 대 한 작업을 수행할 수 있습니다 **ForEach** 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="b4c74-145">Hello 범위 내에서 실패 한 작업의 응답 본문 hello 함께 HTTP POST 요청을 전송 하는 자세한 설명이 나옵니다 예로 `My_Scope`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="b4c74-146">어떤 일이 생기 자세한 연습 toodescribe 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="b4c74-147">내의 모든 작업의 tooget hello 결과 `My_Scope`, hello **필터 배열** 작업 필터 `@result('My_Scope')`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="b4c74-148">에 대 한 조건 hello **필터 배열** 는 임의의 `@result()` 너무 상태를 가진 항목을`Failed`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="b4c74-149">이 상태 필터에서 모든 작업 결과 사용 하 여 hello 배열 `My_Scope` tooan 배열 된 작업 결과 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="b4c74-150">수행는 **각** hello에 대 한 작업 **필터링 배열** 를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="b4c74-151">이 단계는 이전에 필터링된 실패한 작업 결과 *각각에 대해* 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="b4c74-152">Hello 범위에 단일 작업에 실패 한 경우 hello hello에서 동작 `foreach` 한 번만 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="b4c74-153">많은 실패한 작업에서 오류당 하나의 작업이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="b4c74-154">Hello에 HTTP POST를 보낼 `foreach` 응답 본문 항목 또는 `@item()['outputs']['body']`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="b4c74-155">hello `@result()` 항목 셰이프는 동일 hello로 hello `@actions()` , 모양 지정 및 구문 분석할 수 있는 hello 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="b4c74-156">Hello 실패 한 동작 이름 가진 두 개의 사용자 지정 헤더 포함 `@item()['name']` hello 실패 추적 ID는 실행된 된 클라이언트 및 `@item()['clientTrackingId']`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="b4c74-157">참조용으로 다음은 예제는 단일 `@result()` hello를 보여 주는 항목 `name`, `body`, 및 `clientTrackingId` hello 이전 예제에서 구문 분석 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="b4c74-158">`foreach`의 외부에서 `@result()`가 이러한 개체의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="b4c74-159">tooperform 다른 예외 처리 패턴 앞에 표시 된 hello 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="b4c74-160">작업 실패의 전체 필터링 된 배열을 hello를 허용 하는 hello 다루지 처리 예외 하나 tooexecute을 선택 하 고 hello 제거 수 `foreach`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="b4c74-161">Hello에서 다른 유용한 속성을 포함할 수도 있습니다 `@result()` 앞에 표시 된 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="b4c74-162">Azure 진단 및 원격 분석</span><span class="sxs-lookup"><span data-stu-id="b4c74-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="b4c74-163">hello 이전 패턴은 훌륭한 방법 toohandle 오류와 예외는 실행 내에서 하지만 또한 식별 하 고 자체적으로 실행 하는 hello와 무관 tooerrors 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="b4c74-164">[Azure 진단](../logic-apps/logic-apps-monitor-your-logic-apps.md) 모든 워크플로 (실행 및 작업에 대 한 모든 상태를 포함 하 여) 이벤트 tooan Azure 저장소 계정 또는 Azure 이벤트 허브는 간단한 방법을 toosend를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="b4c74-165">tooevaluate 실행 상태, hello 로그 및 메트릭, 모니터링 하거나 원하는 모니터링 도구에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="b4c74-166">한 가지 가능한 옵션은 toostream에 Azure 이벤트 허브를 통해 모든 hello 이벤트 [스트림 분석](https://azure.microsoft.com/services/stream-analytics/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="b4c74-167">스트림 분석에서 작성할 수 있습니다 모든 비정상, 평균 또는 오류 오프 라이브 쿼리 hello에서 진단 로그.</span><span class="sxs-lookup"><span data-stu-id="b4c74-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="b4c74-168">스트림 분석에는 큐, 항목, SQL, Azure Cosmos DB 및 Power BI와 같은 데이터 원본 tooother 출력할 쉽게 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c74-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4c74-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4c74-169">Next Steps</span></span>

* [<span data-ttu-id="b4c74-170">고객이 Azure Logic Apps의 오류 처리를 빌드하는 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c74-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="b4c74-171">논리 앱 예제 및 시나리오 더 찾아보기</span><span class="sxs-lookup"><span data-stu-id="b4c74-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="b4c74-172">Toocreate 논리 앱에 대 한 배포를 자동화 하는 방법을 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="b4c74-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="b4c74-173">Visual Studio에서 논리 앱 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="b4c74-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
