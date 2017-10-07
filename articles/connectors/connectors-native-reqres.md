---
title: "aaaUse 요청 및 응답 동작 | Microsoft Docs"
description: "Hello 요청 및 응답 트리거와 작업이 바뀐 Azure 논리 앱에서의 개요"
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
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="e2fbc-103">Hello 요청 및 응답 구성 요소 시작</span><span class="sxs-lookup"><span data-stu-id="e2fbc-103">Get started with hello request and response components</span></span>
<span data-ttu-id="e2fbc-104">Hello 요청 및 응답의에서 구성 요소와 논리 앱을 실시간으로 tooevents에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="e2fbc-105">예를 들어 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-105">For example, you can:</span></span>

* <span data-ttu-id="e2fbc-106">논리 앱을 통해 온-프레미스 데이터베이스에서 데이터 tooan HTTP 요청에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="e2fbc-107">외부 웹후크 이벤트에서 논리 앱을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="e2fbc-108">다른 논리 앱 내에서 요청 및 응답 작업으로 논리 앱을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="e2fbc-109">hello 요청 및 응답 작업을 사용 하 여 논리 앱의 시작 tooget 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="e2fbc-110">HTTP 요청 트리거 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e2fbc-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="e2fbc-111">트리거는 사용 되는 toostart hello 워크플로 논리 앱에 정의 된 일 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="e2fbc-112">[트리거에 대해 자세히 알아보세요.](connectors-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e2fbc-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="e2fbc-113">시퀀스는 HTTP tooset hello 논리가 응용 프로그램 디자이너에서에서 요청 하는 방법을의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="e2fbc-114">Hello 트리거 추가 **요청-때 HTTP 요청을 받으면** 논리 앱에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="e2fbc-115">JSON 스키마를 선택적으로 제공할 수 있습니다 (같은 도구를 사용 하 여 [JSONSchema.net](http://jsonschema.net)) hello 요청 본문에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="e2fbc-116">따라서 hello HTTP 요청에서 속성에 대 한 hello 디자이너 toogenerate 토큰 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="e2fbc-117">Hello 논리 앱을 저장할 수 있도록 다른 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="e2fbc-118">Hello 논리 앱을 저장 한 후 hello 요청 카드에서 hello HTTP 요청 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="e2fbc-119">HTTP POST (같은 도구를 사용할 수 있습니다 [우체부](https://www.getpostman.com/)) toohello URL 트리거 hello 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="e2fbc-120">응답 작업을 정의 하지 않으면 한 `202 ACCEPTED` 응답 toohello 호출자에 게 즉시 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="e2fbc-121">Hello 응답 동작 toocustomize 응답을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![응답 트리거](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="e2fbc-123">HTTP 응답 동작 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e2fbc-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="e2fbc-124">HTTP 응답 동작 hello HTTP 요청에 의해 트리거되는 워크플로에서 사용 하는 경우에 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="e2fbc-125">응답 작업을 정의 하지 않으면 한 `202 ACCEPTED` 응답 toohello 호출자에 게 즉시 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="e2fbc-126">Hello 워크플로 내에서 모든 단계에서 응답 동작을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="e2fbc-127">hello 논리 앱만 hello 들어오는 요청을 열어 둡니다 응답에 대 일 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="e2fbc-128">Hello 워크플로에서 보낸 응답이 없는 (응답 동작에에서 있는 경우 hello 정의), 1 분 후에 `504 GATEWAY TIMEOUT` toohello 호출자에 게 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="e2fbc-129">다음은 어떻게 tooadd HTTP 응답 동작:</span><span class="sxs-lookup"><span data-stu-id="e2fbc-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="e2fbc-130">선택 hello **새 단계** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="e2fbc-131">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="e2fbc-132">Hello 동작 검색 상자에 입력 **응답** toolist hello 응답 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![Hello 응답 동작을 선택 합니다.](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="e2fbc-134">Hello HTTP 응답 메시지에 필요한 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![전체 hello 응답 동작](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="e2fbc-136">Hello 도구 모음 toosave와 여 논리 앱에서 모두 저장 hello 왼쪽 위 모퉁이 클릭 하 고 게시 (활성화).</span><span class="sxs-lookup"><span data-stu-id="e2fbc-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="e2fbc-137">요청 트리거</span><span class="sxs-lookup"><span data-stu-id="e2fbc-137">Request trigger</span></span>
<span data-ttu-id="e2fbc-138">이 커넥터가 지 원하는 hello 트리거에 대 한 hello 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="e2fbc-139">단일 요청 트리거가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-139">There is a single request trigger.</span></span>

| <span data-ttu-id="e2fbc-140">트리거</span><span class="sxs-lookup"><span data-stu-id="e2fbc-140">Trigger</span></span> | <span data-ttu-id="e2fbc-141">설명</span><span class="sxs-lookup"><span data-stu-id="e2fbc-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e2fbc-142">요청</span><span class="sxs-lookup"><span data-stu-id="e2fbc-142">Request</span></span> |<span data-ttu-id="e2fbc-143">HTTP 요청을 받을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="e2fbc-144">응답 작업</span><span class="sxs-lookup"><span data-stu-id="e2fbc-144">Response action</span></span>
<span data-ttu-id="e2fbc-145">이 커넥터가 지 원하는 hello 동작에 대 한 hello 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="e2fbc-146">요청 트리거와 함께 나올 때만 사용할 수 있는 단일 응답 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="e2fbc-147">작업</span><span class="sxs-lookup"><span data-stu-id="e2fbc-147">Action</span></span> | <span data-ttu-id="e2fbc-148">설명</span><span class="sxs-lookup"><span data-stu-id="e2fbc-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e2fbc-149">응답</span><span class="sxs-lookup"><span data-stu-id="e2fbc-149">Response</span></span> |<span data-ttu-id="e2fbc-150">응답 toohello HTTP 요청 상관 관계를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="e2fbc-151">트리거 및 작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e2fbc-151">Trigger and action details</span></span>
<span data-ttu-id="e2fbc-152">hello 다음 표에서 hello hello 트리거 및 작업에 대 한 입력된 필드에 설명 하 고 해당 출력 세부 정보를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="e2fbc-153">요청 트리거</span><span class="sxs-lookup"><span data-stu-id="e2fbc-153">Request trigger</span></span>
<span data-ttu-id="e2fbc-154">hello 다음은 들어오는 HTTP 요청에서 트리거 hello에 대 한 입력된 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="e2fbc-155">표시 이름</span><span class="sxs-lookup"><span data-stu-id="e2fbc-155">Display name</span></span> | <span data-ttu-id="e2fbc-156">속성 이름</span><span class="sxs-lookup"><span data-stu-id="e2fbc-156">Property name</span></span> | <span data-ttu-id="e2fbc-157">설명</span><span class="sxs-lookup"><span data-stu-id="e2fbc-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2fbc-158">JSON 스키마</span><span class="sxs-lookup"><span data-stu-id="e2fbc-158">JSON Schema</span></span> |<span data-ttu-id="e2fbc-159">schema</span><span class="sxs-lookup"><span data-stu-id="e2fbc-159">schema</span></span> |<span data-ttu-id="e2fbc-160">hello HTTP 요청 본문의 hello JSON 스키마</span><span class="sxs-lookup"><span data-stu-id="e2fbc-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="e2fbc-161">**출력 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="e2fbc-161">**Output details**</span></span>

<span data-ttu-id="e2fbc-162">hello 요청에 대 한 출력 세부 내용은 hello 다음과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="e2fbc-163">속성 이름</span><span class="sxs-lookup"><span data-stu-id="e2fbc-163">Property name</span></span> | <span data-ttu-id="e2fbc-164">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="e2fbc-164">Data type</span></span> | <span data-ttu-id="e2fbc-165">설명</span><span class="sxs-lookup"><span data-stu-id="e2fbc-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2fbc-166">headers</span><span class="sxs-lookup"><span data-stu-id="e2fbc-166">Headers</span></span> |<span data-ttu-id="e2fbc-167">object</span><span class="sxs-lookup"><span data-stu-id="e2fbc-167">object</span></span> |<span data-ttu-id="e2fbc-168">헤더 요청</span><span class="sxs-lookup"><span data-stu-id="e2fbc-168">Request headers</span></span> |
| <span data-ttu-id="e2fbc-169">본문</span><span class="sxs-lookup"><span data-stu-id="e2fbc-169">Body</span></span> |<span data-ttu-id="e2fbc-170">object</span><span class="sxs-lookup"><span data-stu-id="e2fbc-170">object</span></span> |<span data-ttu-id="e2fbc-171">요청 개체</span><span class="sxs-lookup"><span data-stu-id="e2fbc-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="e2fbc-172">응답 작업</span><span class="sxs-lookup"><span data-stu-id="e2fbc-172">Response action</span></span>
<span data-ttu-id="e2fbc-173">hello 다음은 HTTP 응답 동작 hello에 대 한 입력된 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="e2fbc-174">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="e2fbc-175">표시 이름</span><span class="sxs-lookup"><span data-stu-id="e2fbc-175">Display name</span></span> | <span data-ttu-id="e2fbc-176">속성 이름</span><span class="sxs-lookup"><span data-stu-id="e2fbc-176">Property name</span></span> | <span data-ttu-id="e2fbc-177">설명</span><span class="sxs-lookup"><span data-stu-id="e2fbc-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2fbc-178">상태 코드*</span><span class="sxs-lookup"><span data-stu-id="e2fbc-178">Status Code*</span></span> |<span data-ttu-id="e2fbc-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="e2fbc-179">statusCode</span></span> |<span data-ttu-id="e2fbc-180">hello HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="e2fbc-180">hello HTTP status code</span></span> |
| <span data-ttu-id="e2fbc-181">헤더</span><span class="sxs-lookup"><span data-stu-id="e2fbc-181">Headers</span></span> |<span data-ttu-id="e2fbc-182">headers</span><span class="sxs-lookup"><span data-stu-id="e2fbc-182">headers</span></span> |<span data-ttu-id="e2fbc-183">모든 응답 헤더 tooinclude의 JSON 개체</span><span class="sxs-lookup"><span data-stu-id="e2fbc-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="e2fbc-184">body</span><span class="sxs-lookup"><span data-stu-id="e2fbc-184">Body</span></span> |<span data-ttu-id="e2fbc-185">body</span><span class="sxs-lookup"><span data-stu-id="e2fbc-185">body</span></span> |<span data-ttu-id="e2fbc-186">hello 응답 본문</span><span class="sxs-lookup"><span data-stu-id="e2fbc-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e2fbc-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2fbc-187">Next steps</span></span>
<span data-ttu-id="e2fbc-188">이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e2fbc-189">탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2fbc-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

