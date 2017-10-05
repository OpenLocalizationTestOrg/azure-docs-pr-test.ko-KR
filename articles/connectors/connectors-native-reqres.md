---
title: "요청 및 응답 작업 사용 | Microsoft Docs"
description: "Azure 논리 앱의 요청, 응답 트리거 및 작업에 대한 개요"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e45b07d709927af64cfba28dfb0d8ee9cb8893b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-request-and-response-components"></a><span data-ttu-id="3f5e5-103">요청 및 응답 구성 요소 시작</span><span class="sxs-lookup"><span data-stu-id="3f5e5-103">Get started with the request and response components</span></span>
<span data-ttu-id="3f5e5-104">논리 앱의 요청 및 응답 구성 요소를 사용하여 이벤트에 실시간으로 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-104">With the request and response components in a logic app, you can respond in real time to events.</span></span>

<span data-ttu-id="3f5e5-105">예를 들어 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-105">For example, you can:</span></span>

* <span data-ttu-id="3f5e5-106">논리 앱을 통해 온-프레미스 데이터베이스의 데이터를 사용하여 HTTP 요청에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="3f5e5-107">외부 웹후크 이벤트에서 논리 앱을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="3f5e5-108">다른 논리 앱 내에서 요청 및 응답 작업으로 논리 앱을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="3f5e5-109">논리 앱에서 요처 및 응답 작업 사용을 시작하려면 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-request-trigger"></a><span data-ttu-id="3f5e5-110">HTTP 요청 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="3f5e5-110">Use the HTTP Request trigger</span></span>
<span data-ttu-id="3f5e5-111">트리거는 논리 앱에서 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="3f5e5-112">[트리거에 대해 자세히 알아보세요](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f5e5-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="3f5e5-113">논리 앱 디자이너에서 HTTP 요청을 설정하는 방법의 예제 시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span></span>

1. <span data-ttu-id="3f5e5-114">논리 앱에서 **요청 - HTTP 요청을 받은 경우** 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="3f5e5-115">요청 본문에 대해 JSON 스키마를 선택적으로 제공할 수 있습니다( [JSONSchema.net](http://jsonschema.net)과 같은 도구 사용).</span><span class="sxs-lookup"><span data-stu-id="3f5e5-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span></span> <span data-ttu-id="3f5e5-116">이렇게 하면 디자이너가 HTTP 요청에서 속성에 대한 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-116">This allows the designer to generate tokens for properties in the HTTP request.</span></span>
2. <span data-ttu-id="3f5e5-117">논리 앱을 저장할 수 있도록 다른 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-117">Add another action so that you can save the logic app.</span></span>
3. <span data-ttu-id="3f5e5-118">논리 앱을 저장한 후 요청 카드에서 HTTP 요청 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-118">After saving the logic app, you can get the HTTP request URL from the request card.</span></span>
4. <span data-ttu-id="3f5e5-119">URL에 대한 HTTP POST( [Postman](https://www.getpostman.com/)과 같은 도구 사용)는 논리 앱을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="3f5e5-120">응답 작업을 정의하지 않으면 `202 ACCEPTED` 응답이 호출자에게 즉시 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span> <span data-ttu-id="3f5e5-121">응답 작업을 사용하여 응답을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-121">You can use the response action to customize a response.</span></span>
> 
> 

![응답 트리거](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a><span data-ttu-id="3f5e5-123">HTTP 응답 작업 사용</span><span class="sxs-lookup"><span data-stu-id="3f5e5-123">Use the HTTP Response action</span></span>
<span data-ttu-id="3f5e5-124">HTTP 응답 작업은 HTTP 요청에 의해 트리거되는 워크플로에서 사용할 때만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="3f5e5-125">응답 작업을 정의하지 않으면 `202 ACCEPTED` 응답이 호출자에게 즉시 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span>  <span data-ttu-id="3f5e5-126">응답 작업은 워크플로 내의 어느 단계에도 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-126">You can add a response action at any step within the workflow.</span></span> <span data-ttu-id="3f5e5-127">논리 앱은 들어오는 요청이 있을 때 응답을 받기 위해 1분 동안만 열어둡니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-127">The logic app only keeps the incoming request open for one minute for a response.</span></span>  <span data-ttu-id="3f5e5-128">1분 후에 워크플로에서 전송된 응답이 없으면(정의에는 응답 작업이 있음) `504 GATEWAY TIMEOUT` 이 호출자에게 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span></span>

<span data-ttu-id="3f5e5-129">HTTP 응답 작업을 추가하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-129">Here's how to add an HTTP Response action:</span></span>

1. <span data-ttu-id="3f5e5-130">**새 단계** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-130">Select the **New Step** button.</span></span>
2. <span data-ttu-id="3f5e5-131">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="3f5e5-132">작업 검색 상자에 **response** 를 입력하여 응답 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-132">In the action search box, type **response** to list the Response action.</span></span>
   
    ![응답 작업 선택](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="3f5e5-134">HTTP 응답 메시지에 필요한 모든 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-134">Add in any parameters that are required for the HTTP response message.</span></span>
   
    ![응답 작업 완료](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="3f5e5-136">도구 모음의 왼쪽 위 모서리를 클릭하여 저장하면 논리 앱이 저장하고 게시합니다(활성화).</span><span class="sxs-lookup"><span data-stu-id="3f5e5-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="3f5e5-137">요청 트리거</span><span class="sxs-lookup"><span data-stu-id="3f5e5-137">Request trigger</span></span>
<span data-ttu-id="3f5e5-138">여기에는 이 커넥터가 지원하는 트리거에 대한 세부 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-138">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="3f5e5-139">단일 요청 트리거가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-139">There is a single request trigger.</span></span>

| <span data-ttu-id="3f5e5-140">트리거</span><span class="sxs-lookup"><span data-stu-id="3f5e5-140">Trigger</span></span> | <span data-ttu-id="3f5e5-141">설명</span><span class="sxs-lookup"><span data-stu-id="3f5e5-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3f5e5-142">요청</span><span class="sxs-lookup"><span data-stu-id="3f5e5-142">Request</span></span> |<span data-ttu-id="3f5e5-143">HTTP 요청을 받을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="3f5e5-144">응답 작업</span><span class="sxs-lookup"><span data-stu-id="3f5e5-144">Response action</span></span>
<span data-ttu-id="3f5e5-145">여기에는 이 커넥터가 지원하는 작업에 대한 세부 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-145">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="3f5e5-146">요청 트리거와 함께 나올 때만 사용할 수 있는 단일 응답 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="3f5e5-147">작업</span><span class="sxs-lookup"><span data-stu-id="3f5e5-147">Action</span></span> | <span data-ttu-id="3f5e5-148">설명</span><span class="sxs-lookup"><span data-stu-id="3f5e5-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3f5e5-149">response</span><span class="sxs-lookup"><span data-stu-id="3f5e5-149">Response</span></span> |<span data-ttu-id="3f5e5-150">상호 관련된 HTTP 요청에 대한 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-150">Returns a response to the correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="3f5e5-151">트리거 및 작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="3f5e5-151">Trigger and action details</span></span>
<span data-ttu-id="3f5e5-152">다음 표는 트리거 및 작업에 대한 입력 필드와 해당 출력 세부 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="3f5e5-153">요청 트리거</span><span class="sxs-lookup"><span data-stu-id="3f5e5-153">Request trigger</span></span>
<span data-ttu-id="3f5e5-154">다음은 들어오는 HTTP 요청의 트리거에 대한 입력 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-154">The following is an input field for the trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="3f5e5-155">표시 이름</span><span class="sxs-lookup"><span data-stu-id="3f5e5-155">Display name</span></span> | <span data-ttu-id="3f5e5-156">속성 이름</span><span class="sxs-lookup"><span data-stu-id="3f5e5-156">Property name</span></span> | <span data-ttu-id="3f5e5-157">설명</span><span class="sxs-lookup"><span data-stu-id="3f5e5-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f5e5-158">JSON 스키마</span><span class="sxs-lookup"><span data-stu-id="3f5e5-158">JSON Schema</span></span> |<span data-ttu-id="3f5e5-159">schema</span><span class="sxs-lookup"><span data-stu-id="3f5e5-159">schema</span></span> |<span data-ttu-id="3f5e5-160">HTTP 요청 본문의 JSON 스키마</span><span class="sxs-lookup"><span data-stu-id="3f5e5-160">The JSON schema of the HTTP request body</span></span> |

<br>

<span data-ttu-id="3f5e5-161">**출력 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="3f5e5-161">**Output details**</span></span>

<span data-ttu-id="3f5e5-162">다음은 요청에 대한 출력 세부 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-162">The following are output details for the request.</span></span>

| <span data-ttu-id="3f5e5-163">속성 이름</span><span class="sxs-lookup"><span data-stu-id="3f5e5-163">Property name</span></span> | <span data-ttu-id="3f5e5-164">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="3f5e5-164">Data type</span></span> | <span data-ttu-id="3f5e5-165">설명</span><span class="sxs-lookup"><span data-stu-id="3f5e5-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f5e5-166">headers</span><span class="sxs-lookup"><span data-stu-id="3f5e5-166">Headers</span></span> |<span data-ttu-id="3f5e5-167">object</span><span class="sxs-lookup"><span data-stu-id="3f5e5-167">object</span></span> |<span data-ttu-id="3f5e5-168">헤더 요청</span><span class="sxs-lookup"><span data-stu-id="3f5e5-168">Request headers</span></span> |
| <span data-ttu-id="3f5e5-169">본문</span><span class="sxs-lookup"><span data-stu-id="3f5e5-169">Body</span></span> |<span data-ttu-id="3f5e5-170">object</span><span class="sxs-lookup"><span data-stu-id="3f5e5-170">object</span></span> |<span data-ttu-id="3f5e5-171">요청 개체</span><span class="sxs-lookup"><span data-stu-id="3f5e5-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="3f5e5-172">응답 작업</span><span class="sxs-lookup"><span data-stu-id="3f5e5-172">Response action</span></span>
<span data-ttu-id="3f5e5-173">다음은 HTTP 응답 작업에 대한 입력 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-173">The following are input fields for the HTTP Response action.</span></span> <span data-ttu-id="3f5e5-174">A*는 필수 필드 임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="3f5e5-175">표시 이름</span><span class="sxs-lookup"><span data-stu-id="3f5e5-175">Display name</span></span> | <span data-ttu-id="3f5e5-176">속성 이름</span><span class="sxs-lookup"><span data-stu-id="3f5e5-176">Property name</span></span> | <span data-ttu-id="3f5e5-177">설명</span><span class="sxs-lookup"><span data-stu-id="3f5e5-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f5e5-178">상태 코드*</span><span class="sxs-lookup"><span data-stu-id="3f5e5-178">Status Code*</span></span> |<span data-ttu-id="3f5e5-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="3f5e5-179">statusCode</span></span> |<span data-ttu-id="3f5e5-180">HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="3f5e5-180">The HTTP status code</span></span> |
| <span data-ttu-id="3f5e5-181">헤더</span><span class="sxs-lookup"><span data-stu-id="3f5e5-181">Headers</span></span> |<span data-ttu-id="3f5e5-182">헤더</span><span class="sxs-lookup"><span data-stu-id="3f5e5-182">headers</span></span> |<span data-ttu-id="3f5e5-183">포함할 응답 헤더의 JSON 개체</span><span class="sxs-lookup"><span data-stu-id="3f5e5-183">A JSON object of any response headers to include</span></span> |
| <span data-ttu-id="3f5e5-184">본문</span><span class="sxs-lookup"><span data-stu-id="3f5e5-184">Body</span></span> |<span data-ttu-id="3f5e5-185">본문</span><span class="sxs-lookup"><span data-stu-id="3f5e5-185">body</span></span> |<span data-ttu-id="3f5e5-186">응답 본문</span><span class="sxs-lookup"><span data-stu-id="3f5e5-186">The response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3f5e5-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f5e5-187">Next steps</span></span>
<span data-ttu-id="3f5e5-188">이제 플랫폼을 사용해 보고 [논리 앱을 만듭니다](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3f5e5-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="3f5e5-189">[API 목록](apis-list.md)에서 논리 앱의 사용 가능한 다른 커넥터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f5e5-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

