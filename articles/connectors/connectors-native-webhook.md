---
title: "Azure 논리 앱에 대 한 aaaWebhook 커넥터 | Microsoft Docs"
description: "어떻게 toouse webhook 작업 트리거 tooperform 작업 같은 및 필터 배열에서 논리 앱"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a><span data-ttu-id="47720-103">Hello webhook 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="47720-103">Get started with hello webhook connector</span></span>

<span data-ttu-id="47720-104">Hello webhook 동작 및 트리거를 시작, 일시 중지 및 흐름 tooperform 이러한 작업을 다시 시작 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47720-104">With hello webhook action and trigger, you can start, pause, and resume flows tooperform these tasks:</span></span>

* <span data-ttu-id="47720-105">항목이 수신되자마자 [Azure 이벤트 허브](https://github.com/logicappsio/EventHubAPI)에서 트리거</span><span class="sxs-lookup"><span data-stu-id="47720-105">Trigger from an [Azure Event Hub](https://github.com/logicappsio/EventHubAPI) when an item is received</span></span>
* <span data-ttu-id="47720-106">워크플로를 계속하기 전에 승인을 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-106">Wait for an approval before continuing a workflow</span></span>

<span data-ttu-id="47720-107">에 대 한 자세한 내용은 [어떻게 toocreate 여 webhook을 사용할지를 지 원하는 사용자 지정 Api](../logic-apps/logic-apps-create-api-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-107">Learn more about [how toocreate custom APIs that support a webhook](../logic-apps/logic-apps-create-api-app.md).</span></span>

## <a name="use-hello-webhook-trigger"></a><span data-ttu-id="47720-108">Hello webhook 트리거를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="47720-108">Use hello webhook trigger</span></span>

<span data-ttu-id="47720-109">[*트리거*](connectors-overview.md)는 논리 앱에서 워크플로를 시작하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="47720-109">A [*trigger*](connectors-overview.md) is an event that starts a logic app workflow.</span></span> <span data-ttu-id="47720-110">웹후크 트리거는 이벤트 기반이며 새 항목에 대한 폴링에 의존하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47720-110">A webhook trigger is event-based and doesn't rely on polling for new items.</span></span> <span data-ttu-id="47720-111">Hello 처럼 [요청 트리거](connectors-native-reqres.md), hello 논리 앱 hello 이벤트가 발생 한다고 즉시 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-111">Like hello [request trigger](connectors-native-reqres.md), hello logic app fires hello instant that an event happens.</span></span> <span data-ttu-id="47720-112">hello webhook 트리거 등록을 *콜백 URL* tooa 서비스 및 사용 하 여 해당 URL toofire hello 논리 앱으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-112">hello webhook trigger registers a *callback URL* tooa service and uses that URL toofire hello logic app as needed.</span></span>

<span data-ttu-id="47720-113">Tooset HTTP hello 논리가 응용 프로그램 디자이너에서에서 발생 하는 방법을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="47720-113">Here's an example that shows how tooset up an HTTP trigger in hello Logic App Designer.</span></span> <span data-ttu-id="47720-114">hello 단계 나 있다고도 가정할 수를 이미 배포한 hello 뒤에 오는 API에 액세스 하는 [webhook 구독 및 논리 앱에서 패턴을 구독 취소](../logic-apps/logic-apps-create-api-app.md#webhook-triggers)합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-114">hello steps assume that you have already deployed or are accessing an API that follows hello [webhook subscribe and unsubscribe pattern in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-triggers).</span></span> <span data-ttu-id="47720-115">hello 구독 호출 논리 앱이 새 webhook와 함께 저장 또는 사용 안 함된 tooenabled에서 전환 될 때마다 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="47720-115">hello subscribe call is made whenever a logic app is saved with a new webhook, or switched from disabled tooenabled.</span></span> <span data-ttu-id="47720-116">hello 호출 구독 취소 논리 앱 webhook 트리거 제거 및 저장 하거나 활성화 된 toodisabled에서 전환 하는 경우에 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="47720-116">hello unsubscribe call is made when a logic app webhook trigger is removed and saved, or switched from enabled toodisabled.</span></span>

<span data-ttu-id="47720-117">**tooadd hello webhook 트리거**</span><span class="sxs-lookup"><span data-stu-id="47720-117">**tooadd hello webhook trigger**</span></span>

1. <span data-ttu-id="47720-118">Hello 추가 **HTTP Webhook** 트리거 논리 앱의 첫 번째 단계로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-118">Add hello **HTTP Webhook** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="47720-119">Hello webhook 구독 하 고 호출 구독 취소에 대 한 hello 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-119">Fill in hello parameters for hello webhook subscribe and unsubscribe calls.</span></span>

   <span data-ttu-id="47720-120">이 단계 hello hello와 같은 패턴을 따르는 [HTTP 동작](connectors-native-http.md) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="47720-120">This step follows hello same pattern as hello [HTTP action](connectors-native-http.md) format.</span></span>

     ![HTTP 트리거](./media/connectors-native-webhook/using-trigger.png)

3. <span data-ttu-id="47720-122">하나 이상의 동작을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-122">Add at least one action.</span></span>
4. <span data-ttu-id="47720-123">클릭 **저장** toopublish hello 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="47720-123">Click **Save** toopublish hello logic app.</span></span> <span data-ttu-id="47720-124">이 단계 호출 hello 끝점 hello 콜백 필요한 URL tootrigger이 논리 앱을 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-124">This step calls hello subscribe endpoint with hello callback URL needed tootrigger this logic app.</span></span>
5. <span data-ttu-id="47720-125">때마다 서비스는 hello는 `HTTP POST` toohello 콜백 URL, 논리 앱 실행 되 면 hello 및 hello 요청으로 전달 되는 모든 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-125">Whenever hello service makes an `HTTP POST` toohello callback URL, hello logic app fires, and includes any data passed into hello request.</span></span>

## <a name="use-hello-webhook-action"></a><span data-ttu-id="47720-126">Hello webhook 작업을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="47720-126">Use hello webhook action</span></span>

<span data-ttu-id="47720-127">[ *동작* ](connectors-overview.md) 작업에 의해 수행 되며 hello 워크플로 논리 앱에서 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-127">An [*action*](connectors-overview.md) is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="47720-128">Webhook 작업을 등록 한 *콜백 URL* 서비스와 hello URL이 다시 시작 하기 전에 호출 될 때까지 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-128">A webhook action registers a *callback URL* with a service and waits until hello URL is called before resuming.</span></span> <span data-ttu-id="47720-129">hello ["승인 전자 메일 보내기"](connectors-create-api-office365-outlook.md) 은이 패턴을 따르는 커넥터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="47720-129">hello ["Send Approval Email"](connectors-create-api-office365-outlook.md) is an example of a connector that follows this pattern.</span></span> <span data-ttu-id="47720-130">Hello webhook 작업을 통해 모든 서비스에이 패턴을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47720-130">You can extend this pattern into any service through hello webhook action.</span></span> 

<span data-ttu-id="47720-131">webhook 작업이 tooset 논리가 응용 프로그램 디자이너 hello 하는 방법을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="47720-131">Here's an example that shows how tooset up a webhook action in hello Logic App Designer.</span></span> <span data-ttu-id="47720-132">이 단계를 이미 배포한 하거나 hello 뒤에 오는 API에 액세스 하는 가정 [webhook 구독 및 논리 앱에서 사용 된 패턴을 구독 취소](../logic-apps/logic-apps-create-api-app.md#webhook-actions)합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-132">These steps assume that you have already deployed or are accessing an API that follows hello [webhook subscribe and unsubscribe pattern used in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-actions).</span></span> <span data-ttu-id="47720-133">hello 구독 호출 논리 앱 hello webhook 작업을 실행할 때 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="47720-133">hello subscribe call is made when a logic app executes hello webhook action.</span></span> <span data-ttu-id="47720-134">hello 구독 호출을 취소할 때 실행 되는 응답을 기다리는 동안 취소 되거나 hello 논리 하기 전에 응용 프로그램 시간을 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-134">hello unsubscribe call is made when a run is canceled while waiting for a response, or before hello logic app times out.</span></span>

<span data-ttu-id="47720-135">**tooadd webhook 작업**</span><span class="sxs-lookup"><span data-stu-id="47720-135">**tooadd a webhook action**</span></span>

1. <span data-ttu-id="47720-136">**다음 단계** > **동작 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-136">Choose **New Step** > **Add an action**.</span></span>

2. <span data-ttu-id="47720-137">Hello 검색 상자에 입력 "webhook" toofind hello **HTTP Webhook** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-137">In hello search box, type "webhook" toofind hello **HTTP Webhook** action.</span></span>

    ![쿼리 동작 선택](./media/connectors-native-webhook/using-action-1.png)

3. <span data-ttu-id="47720-139">Hello webhook 구독 하 고 호출 구독 취소에 대 한 hello 매개 변수를 입력</span><span class="sxs-lookup"><span data-stu-id="47720-139">Fill in hello parameters for hello webhook subscribe and unsubscribe calls</span></span>

   <span data-ttu-id="47720-140">이 단계 hello hello와 같은 패턴을 따르는 [HTTP 동작](connectors-native-http.md) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="47720-140">This step follows hello same pattern as hello [HTTP action](connectors-native-http.md) format.</span></span>

     ![쿼리 동작 완료](./media/connectors-native-webhook/using-action-2.png)
   
   <span data-ttu-id="47720-142">런타임 시 hello 논리 앱 호출 hello 해당 단계에 도달한 후 끝점을 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-142">At runtime, hello logic app calls hello subscribe endpoint after reaching that step.</span></span>

4. <span data-ttu-id="47720-143">클릭 **저장** toopublish hello 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="47720-143">Click **Save** toopublish hello logic app.</span></span>

## <a name="technical-details"></a><span data-ttu-id="47720-144">기술 세부 정보</span><span class="sxs-lookup"><span data-stu-id="47720-144">Technical details</span></span>

<span data-ttu-id="47720-145">여기에 자세한 내용이 hello 트리거 및 작업에 대 한 해당 webhook을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-145">Here are more details about hello triggers and actions that webhook supports.</span></span>

## <a name="webhook-triggers"></a><span data-ttu-id="47720-146">웹후크 트리거</span><span class="sxs-lookup"><span data-stu-id="47720-146">Webhook triggers</span></span>

| <span data-ttu-id="47720-147">작업</span><span class="sxs-lookup"><span data-stu-id="47720-147">Action</span></span> | <span data-ttu-id="47720-148">설명</span><span class="sxs-lookup"><span data-stu-id="47720-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47720-149">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="47720-149">HTTP Webhook</span></span> |<span data-ttu-id="47720-150">필요에 따라 hello URL toofire 논리 앱을 호출할 수 있는 콜백 URL tooa 서비스를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-150">Subscribe a callback URL tooa service that can call hello URL toofire logic app as needed.</span></span> |

### <a name="trigger-details"></a><span data-ttu-id="47720-151">트리거 세부 정보</span><span class="sxs-lookup"><span data-stu-id="47720-151">Trigger details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="47720-152">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="47720-152">HTTP Webhook</span></span>

<span data-ttu-id="47720-153">필요에 따라 hello URL toofire 논리 앱을 호출할 수 있는 콜백 URL tooa 서비스를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-153">Subscribe a callback URL tooa service that can call hello URL toofire logic app as needed.</span></span>
<span data-ttu-id="47720-154">*는 필수 필드를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-154">An * means required field.</span></span>

| <span data-ttu-id="47720-155">표시 이름</span><span class="sxs-lookup"><span data-stu-id="47720-155">Display Name</span></span> | <span data-ttu-id="47720-156">속성 이름</span><span class="sxs-lookup"><span data-stu-id="47720-156">Property Name</span></span> | <span data-ttu-id="47720-157">설명</span><span class="sxs-lookup"><span data-stu-id="47720-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47720-158">구독 메서드*</span><span class="sxs-lookup"><span data-stu-id="47720-158">Subscribe Method*</span></span> |<span data-ttu-id="47720-159">메서드</span><span class="sxs-lookup"><span data-stu-id="47720-159">method</span></span> |<span data-ttu-id="47720-160">구독 요청에 대 한 HTTP 메서드 toouse</span><span class="sxs-lookup"><span data-stu-id="47720-160">HTTP Method toouse for subscribe request</span></span> |
| <span data-ttu-id="47720-161">구독 URI*</span><span class="sxs-lookup"><span data-stu-id="47720-161">Subscribe URI*</span></span> |<span data-ttu-id="47720-162">uri</span><span class="sxs-lookup"><span data-stu-id="47720-162">uri</span></span> |<span data-ttu-id="47720-163">구독 요청에 대 한 HTTP URI toouse</span><span class="sxs-lookup"><span data-stu-id="47720-163">HTTP URI toouse for subscribe request</span></span> |
| <span data-ttu-id="47720-164">구독 취소 메서드*</span><span class="sxs-lookup"><span data-stu-id="47720-164">Unsubscribe Method*</span></span> |<span data-ttu-id="47720-165">메서드</span><span class="sxs-lookup"><span data-stu-id="47720-165">method</span></span> |<span data-ttu-id="47720-166">구독 취소 요청에 대 한 HTTP 메서드 toouse</span><span class="sxs-lookup"><span data-stu-id="47720-166">HTTP method toouse for unsubscribe request</span></span> |
| <span data-ttu-id="47720-167">구독 취소 URI*</span><span class="sxs-lookup"><span data-stu-id="47720-167">Unsubscribe URI*</span></span> |<span data-ttu-id="47720-168">uri</span><span class="sxs-lookup"><span data-stu-id="47720-168">uri</span></span> |<span data-ttu-id="47720-169">구독 취소 요청에 대 한 HTTP URI toouse</span><span class="sxs-lookup"><span data-stu-id="47720-169">HTTP URI toouse for unsubscribe request</span></span> |
| <span data-ttu-id="47720-170">구독 본문</span><span class="sxs-lookup"><span data-stu-id="47720-170">Subscribe Body</span></span> |<span data-ttu-id="47720-171">body</span><span class="sxs-lookup"><span data-stu-id="47720-171">body</span></span> |<span data-ttu-id="47720-172">구독의 HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="47720-172">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="47720-173">구독 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-173">Subscribe Headers</span></span> |<span data-ttu-id="47720-174">headers</span><span class="sxs-lookup"><span data-stu-id="47720-174">headers</span></span> |<span data-ttu-id="47720-175">구독의 HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-175">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="47720-176">구독 인증</span><span class="sxs-lookup"><span data-stu-id="47720-176">Subscribe Authentication</span></span> |<span data-ttu-id="47720-177">인증</span><span class="sxs-lookup"><span data-stu-id="47720-177">authentication</span></span> |<span data-ttu-id="47720-178">구독에 대 한 HTTP 인증 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-178">HTTP authentication toouse for subscribe.</span></span> <span data-ttu-id="47720-179">자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요.</span><span class="sxs-lookup"><span data-stu-id="47720-179">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="47720-180">구독 취소 본문</span><span class="sxs-lookup"><span data-stu-id="47720-180">Unsubscribe Body</span></span> |<span data-ttu-id="47720-181">body</span><span class="sxs-lookup"><span data-stu-id="47720-181">body</span></span> |<span data-ttu-id="47720-182">구독 취소의 HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="47720-182">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="47720-183">구독 취소 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-183">Unsubscribe Headers</span></span> |<span data-ttu-id="47720-184">headers</span><span class="sxs-lookup"><span data-stu-id="47720-184">headers</span></span> |<span data-ttu-id="47720-185">구독 취소의 HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-185">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="47720-186">구독 취소 인증</span><span class="sxs-lookup"><span data-stu-id="47720-186">Unsubscribe Authentication</span></span> |<span data-ttu-id="47720-187">인증</span><span class="sxs-lookup"><span data-stu-id="47720-187">authentication</span></span> |<span data-ttu-id="47720-188">구독 취소에 대 한 HTTP 인증 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-188">HTTP authentication toouse for unsubscribe.</span></span> <span data-ttu-id="47720-189">자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요.</span><span class="sxs-lookup"><span data-stu-id="47720-189">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="47720-190">**출력 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="47720-190">**Output Details**</span></span>

<span data-ttu-id="47720-191">웹후크 요청</span><span class="sxs-lookup"><span data-stu-id="47720-191">Webhook request</span></span>

| <span data-ttu-id="47720-192">속성 이름</span><span class="sxs-lookup"><span data-stu-id="47720-192">Property Name</span></span> | <span data-ttu-id="47720-193">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="47720-193">Data Type</span></span> | <span data-ttu-id="47720-194">설명</span><span class="sxs-lookup"><span data-stu-id="47720-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47720-195">headers</span><span class="sxs-lookup"><span data-stu-id="47720-195">Headers</span></span> |<span data-ttu-id="47720-196">object</span><span class="sxs-lookup"><span data-stu-id="47720-196">object</span></span> |<span data-ttu-id="47720-197">웹후크 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-197">Webhook request headers</span></span> |
| <span data-ttu-id="47720-198">body</span><span class="sxs-lookup"><span data-stu-id="47720-198">Body</span></span> |<span data-ttu-id="47720-199">object</span><span class="sxs-lookup"><span data-stu-id="47720-199">object</span></span> |<span data-ttu-id="47720-200">웹후크 요청 개체</span><span class="sxs-lookup"><span data-stu-id="47720-200">Webhook request object</span></span> |
| <span data-ttu-id="47720-201">상태 코드</span><span class="sxs-lookup"><span data-stu-id="47720-201">Status Code</span></span> |<span data-ttu-id="47720-202">int</span><span class="sxs-lookup"><span data-stu-id="47720-202">int</span></span> |<span data-ttu-id="47720-203">웹후크 요청 상태 코드</span><span class="sxs-lookup"><span data-stu-id="47720-203">Webhook request status code</span></span> |

## <a name="webhook-actions"></a><span data-ttu-id="47720-204">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="47720-204">Webhook actions</span></span>

| <span data-ttu-id="47720-205">작업</span><span class="sxs-lookup"><span data-stu-id="47720-205">Action</span></span> | <span data-ttu-id="47720-206">설명</span><span class="sxs-lookup"><span data-stu-id="47720-206">Description</span></span> |
| --- | --- |
| <span data-ttu-id="47720-207">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="47720-207">HTTP Webhook</span></span> |<span data-ttu-id="47720-208">Hello URL tooresume 필요에 따라 워크플로 단계를 호출할 수 있는 콜백 URL tooa 서비스를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-208">Subscribe a callback URL tooa service that can call hello URL tooresume a workflow step as needed.</span></span> |

### <a name="action-details"></a><span data-ttu-id="47720-209">작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="47720-209">Action details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="47720-210">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="47720-210">HTTP Webhook</span></span>

<span data-ttu-id="47720-211">Hello URL tooresume 필요에 따라 워크플로 단계를 호출할 수 있는 콜백 URL tooa 서비스를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-211">Subscribe a callback URL tooa service that can call hello URL tooresume a workflow step as needed.</span></span>
<span data-ttu-id="47720-212">*는 필수 필드를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-212">An * means required field.</span></span>

| <span data-ttu-id="47720-213">표시 이름</span><span class="sxs-lookup"><span data-stu-id="47720-213">Display Name</span></span> | <span data-ttu-id="47720-214">속성 이름</span><span class="sxs-lookup"><span data-stu-id="47720-214">Property Name</span></span> | <span data-ttu-id="47720-215">설명</span><span class="sxs-lookup"><span data-stu-id="47720-215">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47720-216">구독 메서드*</span><span class="sxs-lookup"><span data-stu-id="47720-216">Subscribe Method*</span></span> |<span data-ttu-id="47720-217">메서드</span><span class="sxs-lookup"><span data-stu-id="47720-217">method</span></span> |<span data-ttu-id="47720-218">구독 요청에 대 한 HTTP 메서드 toouse</span><span class="sxs-lookup"><span data-stu-id="47720-218">HTTP Method toouse for subscribe request</span></span> |
| <span data-ttu-id="47720-219">구독 URI*</span><span class="sxs-lookup"><span data-stu-id="47720-219">Subscribe URI*</span></span> |<span data-ttu-id="47720-220">uri</span><span class="sxs-lookup"><span data-stu-id="47720-220">uri</span></span> |<span data-ttu-id="47720-221">구독 요청에 대 한 HTTP URI toouse</span><span class="sxs-lookup"><span data-stu-id="47720-221">HTTP URI toouse for subscribe request</span></span> |
| <span data-ttu-id="47720-222">구독 취소 메서드*</span><span class="sxs-lookup"><span data-stu-id="47720-222">Unsubscribe Method*</span></span> |<span data-ttu-id="47720-223">메서드</span><span class="sxs-lookup"><span data-stu-id="47720-223">method</span></span> |<span data-ttu-id="47720-224">구독 취소 요청에 대 한 HTTP 메서드 toouse</span><span class="sxs-lookup"><span data-stu-id="47720-224">HTTP method toouse for unsubscribe request</span></span> |
| <span data-ttu-id="47720-225">구독 취소 URI*</span><span class="sxs-lookup"><span data-stu-id="47720-225">Unsubscribe URI*</span></span> |<span data-ttu-id="47720-226">uri</span><span class="sxs-lookup"><span data-stu-id="47720-226">uri</span></span> |<span data-ttu-id="47720-227">구독 취소 요청에 대 한 HTTP URI toouse</span><span class="sxs-lookup"><span data-stu-id="47720-227">HTTP URI toouse for unsubscribe request</span></span> |
| <span data-ttu-id="47720-228">구독 본문</span><span class="sxs-lookup"><span data-stu-id="47720-228">Subscribe Body</span></span> |<span data-ttu-id="47720-229">body</span><span class="sxs-lookup"><span data-stu-id="47720-229">body</span></span> |<span data-ttu-id="47720-230">구독의 HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="47720-230">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="47720-231">구독 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-231">Subscribe Headers</span></span> |<span data-ttu-id="47720-232">headers</span><span class="sxs-lookup"><span data-stu-id="47720-232">headers</span></span> |<span data-ttu-id="47720-233">구독의 HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-233">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="47720-234">구독 인증</span><span class="sxs-lookup"><span data-stu-id="47720-234">Subscribe Authentication</span></span> |<span data-ttu-id="47720-235">인증</span><span class="sxs-lookup"><span data-stu-id="47720-235">authentication</span></span> |<span data-ttu-id="47720-236">구독에 대 한 HTTP 인증 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-236">HTTP authentication toouse for subscribe.</span></span> <span data-ttu-id="47720-237">자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요.</span><span class="sxs-lookup"><span data-stu-id="47720-237">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="47720-238">구독 취소 본문</span><span class="sxs-lookup"><span data-stu-id="47720-238">Unsubscribe Body</span></span> |<span data-ttu-id="47720-239">body</span><span class="sxs-lookup"><span data-stu-id="47720-239">body</span></span> |<span data-ttu-id="47720-240">구독 취소의 HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="47720-240">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="47720-241">구독 취소 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-241">Unsubscribe Headers</span></span> |<span data-ttu-id="47720-242">headers</span><span class="sxs-lookup"><span data-stu-id="47720-242">headers</span></span> |<span data-ttu-id="47720-243">구독 취소의 HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-243">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="47720-244">구독 취소 인증</span><span class="sxs-lookup"><span data-stu-id="47720-244">Unsubscribe Authentication</span></span> |<span data-ttu-id="47720-245">인증</span><span class="sxs-lookup"><span data-stu-id="47720-245">authentication</span></span> |<span data-ttu-id="47720-246">구독 취소에 대 한 HTTP 인증 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="47720-246">HTTP authentication toouse for unsubscribe.</span></span> <span data-ttu-id="47720-247">자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요.</span><span class="sxs-lookup"><span data-stu-id="47720-247">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="47720-248">**출력 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="47720-248">**Output Details**</span></span>

<span data-ttu-id="47720-249">웹후크 요청</span><span class="sxs-lookup"><span data-stu-id="47720-249">Webhook request</span></span>

| <span data-ttu-id="47720-250">속성 이름</span><span class="sxs-lookup"><span data-stu-id="47720-250">Property Name</span></span> | <span data-ttu-id="47720-251">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="47720-251">Data Type</span></span> | <span data-ttu-id="47720-252">설명</span><span class="sxs-lookup"><span data-stu-id="47720-252">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47720-253">headers</span><span class="sxs-lookup"><span data-stu-id="47720-253">Headers</span></span> |<span data-ttu-id="47720-254">object</span><span class="sxs-lookup"><span data-stu-id="47720-254">object</span></span> |<span data-ttu-id="47720-255">웹후크 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="47720-255">Webhook request headers</span></span> |
| <span data-ttu-id="47720-256">body</span><span class="sxs-lookup"><span data-stu-id="47720-256">Body</span></span> |<span data-ttu-id="47720-257">object</span><span class="sxs-lookup"><span data-stu-id="47720-257">object</span></span> |<span data-ttu-id="47720-258">웹후크 요청 개체</span><span class="sxs-lookup"><span data-stu-id="47720-258">Webhook request object</span></span> |
| <span data-ttu-id="47720-259">상태 코드</span><span class="sxs-lookup"><span data-stu-id="47720-259">Status Code</span></span> |<span data-ttu-id="47720-260">int</span><span class="sxs-lookup"><span data-stu-id="47720-260">int</span></span> |<span data-ttu-id="47720-261">웹후크 요청 상태 코드</span><span class="sxs-lookup"><span data-stu-id="47720-261">Webhook request status code</span></span> |

## <a name="next-steps"></a><span data-ttu-id="47720-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47720-262">Next steps</span></span>

* [<span data-ttu-id="47720-263">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="47720-263">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="47720-264">다른 커넥터 찾기</span><span class="sxs-lookup"><span data-stu-id="47720-264">Find other connectors</span></span>](apis-list.md)