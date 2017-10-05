---
title: "Azure Logic Apps용 웹후크 커넥터 | Microsoft Docs"
description: "웹후크 동작 및 트리거를 사용하여 Logic Apps에서 필터 배열과 같은 동작을 수행하는 방법"
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
ms.openlocfilehash: fbfef291334109c6dcfcde80741874549fb7929f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-webhook-connector"></a><span data-ttu-id="ad5ac-103">웹후크 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="ad5ac-103">Get started with the webhook connector</span></span>

<span data-ttu-id="ad5ac-104">웹후크 동작 및 트리거를 사용하여 다음 작업을 수행하기 위한 흐름을 시작, 일시 중지 및 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-104">With the webhook action and trigger, you can start, pause, and resume flows to perform these tasks:</span></span>

* <span data-ttu-id="ad5ac-105">항목이 수신되자마자 [Azure 이벤트 허브](https://github.com/logicappsio/EventHubAPI)에서 트리거</span><span class="sxs-lookup"><span data-stu-id="ad5ac-105">Trigger from an [Azure Event Hub](https://github.com/logicappsio/EventHubAPI) when an item is received</span></span>
* <span data-ttu-id="ad5ac-106">워크플로를 계속하기 전에 승인을 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-106">Wait for an approval before continuing a workflow</span></span>

<span data-ttu-id="ad5ac-107">[웹후크를 지원하는 사용자 지정 API를 만드는 방법](../logic-apps/logic-apps-create-api-app.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-107">Learn more about [how to create custom APIs that support a webhook](../logic-apps/logic-apps-create-api-app.md).</span></span>

## <a name="use-the-webhook-trigger"></a><span data-ttu-id="ad5ac-108">웹후크 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="ad5ac-108">Use the webhook trigger</span></span>

<span data-ttu-id="ad5ac-109">[*트리거*](connectors-overview.md)는 논리 앱에서 워크플로를 시작하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-109">A [*trigger*](connectors-overview.md) is an event that starts a logic app workflow.</span></span> <span data-ttu-id="ad5ac-110">웹후크 트리거는 이벤트 기반이며 새 항목에 대한 폴링에 의존하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-110">A webhook trigger is event-based and doesn't rely on polling for new items.</span></span> <span data-ttu-id="ad5ac-111">[요청 트리거](connectors-native-reqres.md)와 마찬가지로, 논리 앱은 이벤트가 발생하는 인스턴트를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-111">Like the [request trigger](connectors-native-reqres.md), the logic app fires the instant that an event happens.</span></span> <span data-ttu-id="ad5ac-112">웹후크 트리거는 *콜백 URL*을 서비스에 등록하고 해당 URL을 사용해서 필요에 따라 논리 앱을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-112">The webhook trigger registers a *callback URL* to a service and uses that URL to fire the logic app as needed.</span></span>

<span data-ttu-id="ad5ac-113">논리 앱 디자이너에서 HTTP 트리거를 설정하는 방법을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-113">Here's an example that shows how to set up an HTTP trigger in the Logic App Designer.</span></span> <span data-ttu-id="ad5ac-114">이러한 단계에서는 [Logic Apps에서 사용되는 웹후크 구독 및 구독 취소 패턴](../logic-apps/logic-apps-create-api-app.md#webhook-triggers)을 따라 API를 이미 배포했거나 액세스하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-114">The steps assume that you have already deployed or are accessing an API that follows the [webhook subscribe and unsubscribe pattern in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-triggers).</span></span> <span data-ttu-id="ad5ac-115">구독 호출은 논리 앱이 새 웹후크와 함께 저장되거나 사용 안 함 상태에서 사용 상태로 전환될 때마다 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-115">The subscribe call is made whenever a logic app is saved with a new webhook, or switched from disabled to enabled.</span></span> <span data-ttu-id="ad5ac-116">구독 취소 호출은 논리 앱 웹후크 트리거가 제거 또는 저장되거나 사용 상태에서 사용 안 함 상태로 전환될 때 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-116">The unsubscribe call is made when a logic app webhook trigger is removed and saved, or switched from enabled to disabled.</span></span>

<span data-ttu-id="ad5ac-117">**웹후크 트리거를 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="ad5ac-117">**To add the webhook trigger**</span></span>

1. <span data-ttu-id="ad5ac-118">**HTTP 웹후크** 트리거를 논리 앱의 첫 번째 단계로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-118">Add the **HTTP Webhook** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="ad5ac-119">웹후크 구독 및 구독 취소 호출에 대한 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-119">Fill in the parameters for the webhook subscribe and unsubscribe calls.</span></span>

   <span data-ttu-id="ad5ac-120">이 단계는 [HTTP 동작](connectors-native-http.md) 형식과 동일한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-120">This step follows the same pattern as the [HTTP action](connectors-native-http.md) format.</span></span>

     ![HTTP 트리거](./media/connectors-native-webhook/using-trigger.png)

3. <span data-ttu-id="ad5ac-122">하나 이상의 동작을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-122">Add at least one action.</span></span>
4. <span data-ttu-id="ad5ac-123">**저장**을 클릭하여 논리 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-123">Click **Save** to publish the logic app.</span></span> <span data-ttu-id="ad5ac-124">이 단계를 수행하면 이 Logic App을 트리거하는 데 필요한 콜백 URL을 사용하여 구독 끝점이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-124">This step calls the subscribe endpoint with the callback URL needed to trigger this logic app.</span></span>
5. <span data-ttu-id="ad5ac-125">서비스에서 콜백 URL에 댛 `HTTP POST` 를 수행할 때마다 논리 앱이 실행됩니다(논리 앱에는 요청에 전달된 모든 데이터가 포함됨).</span><span class="sxs-lookup"><span data-stu-id="ad5ac-125">Whenever the service makes an `HTTP POST` to the callback URL, the logic app fires, and includes any data passed into the request.</span></span>

## <a name="use-the-webhook-action"></a><span data-ttu-id="ad5ac-126">웹후크 동작 사용</span><span class="sxs-lookup"><span data-stu-id="ad5ac-126">Use the webhook action</span></span>

<span data-ttu-id="ad5ac-127">[*동작*](connectors-overview.md)은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-127">An [*action*](connectors-overview.md) is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="ad5ac-128">웹후크 동작은 서비스에 *콜백 URL* 을 등록하고, 다시 시작하기 전에 URL이 호출될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-128">A webhook action registers a *callback URL* with a service and waits until the URL is called before resuming.</span></span> <span data-ttu-id="ad5ac-129">["승인 전자 메일 보내기"](connectors-create-api-office365-outlook.md) 는 이 패턴을 따르는 커넥터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-129">The ["Send Approval Email"](connectors-create-api-office365-outlook.md) is an example of a connector that follows this pattern.</span></span> <span data-ttu-id="ad5ac-130">이 패턴을 웹후크 동작을 통해 서비스로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-130">You can extend this pattern into any service through the webhook action.</span></span> 

<span data-ttu-id="ad5ac-131">논리 앱 디자이너에서 웹후크 동작을 설정하는 방법을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-131">Here's an example that shows how to set up a webhook action in the Logic App Designer.</span></span> <span data-ttu-id="ad5ac-132">이러한 단계에서는 [Logic Apps에서 사용되는 웹후크 구독 및 구독 취소 패턴](../logic-apps/logic-apps-create-api-app.md#webhook-actions)을 따라 API를 이미 배포했거나 액세스하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-132">These steps assume that you have already deployed or are accessing an API that follows the [webhook subscribe and unsubscribe pattern used in logic apps](../logic-apps/logic-apps-create-api-app.md#webhook-actions).</span></span> <span data-ttu-id="ad5ac-133">논리 앱이 웹후크 동작을 실행할 때 구독 호출이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-133">The subscribe call is made when a logic app executes the webhook action.</span></span> <span data-ttu-id="ad5ac-134">응답을 기다리는 동안 또는 논리 앱 실행이 시간 초과되기 전에 실행이 취소될 때 구독 취소 호출이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-134">The unsubscribe call is made when a run is canceled while waiting for a response, or before the logic app times out.</span></span>

<span data-ttu-id="ad5ac-135">**웹후크 동작을 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="ad5ac-135">**To add a webhook action**</span></span>

1. <span data-ttu-id="ad5ac-136">**다음 단계** > **동작 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-136">Choose **New Step** > **Add an action**.</span></span>

2. <span data-ttu-id="ad5ac-137">검색 상자에 "웹후크"를 입력하여 **HTTP 웹후크** 동작을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-137">In the search box, type "webhook" to find the **HTTP Webhook** action.</span></span>

    ![쿼리 동작 선택](./media/connectors-native-webhook/using-action-1.png)

3. <span data-ttu-id="ad5ac-139">웹후크 구독 및 구독 취소 호출에 대한 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-139">Fill in the parameters for the webhook subscribe and unsubscribe calls</span></span>

   <span data-ttu-id="ad5ac-140">이 단계는 [HTTP 동작](connectors-native-http.md) 형식과 동일한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-140">This step follows the same pattern as the [HTTP action](connectors-native-http.md) format.</span></span>

     ![쿼리 동작 완료](./media/connectors-native-webhook/using-action-2.png)
   
   <span data-ttu-id="ad5ac-142">런타임 시 논리 앱은 해당 단계에 도달한 후 구독 끝점을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-142">At runtime, the logic app calls the subscribe endpoint after reaching that step.</span></span>

4. <span data-ttu-id="ad5ac-143">**저장**을 클릭하여 논리 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-143">Click **Save** to publish the logic app.</span></span>

## <a name="technical-details"></a><span data-ttu-id="ad5ac-144">기술 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ad5ac-144">Technical details</span></span>

<span data-ttu-id="ad5ac-145">웹후크가 지원하는 트리거 및 동작에 대한 자세한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-145">Here are more details about the triggers and actions that webhook supports.</span></span>

## <a name="webhook-triggers"></a><span data-ttu-id="ad5ac-146">웹후크 트리거</span><span class="sxs-lookup"><span data-stu-id="ad5ac-146">Webhook triggers</span></span>

| <span data-ttu-id="ad5ac-147">작업</span><span class="sxs-lookup"><span data-stu-id="ad5ac-147">Action</span></span> | <span data-ttu-id="ad5ac-148">설명</span><span class="sxs-lookup"><span data-stu-id="ad5ac-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad5ac-149">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="ad5ac-149">HTTP Webhook</span></span> |<span data-ttu-id="ad5ac-150">필요에 따라 URL을 호출할 수 있는 서비스에 대한 콜백 URL을 구독하여 논리 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-150">Subscribe a callback URL to a service that can call the URL to fire logic app as needed.</span></span> |

### <a name="trigger-details"></a><span data-ttu-id="ad5ac-151">트리거 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ad5ac-151">Trigger details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="ad5ac-152">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="ad5ac-152">HTTP Webhook</span></span>

<span data-ttu-id="ad5ac-153">필요에 따라 URL을 호출할 수 있는 서비스에 대한 콜백 URL을 구독하여 논리 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-153">Subscribe a callback URL to a service that can call the URL to fire logic app as needed.</span></span>
<span data-ttu-id="ad5ac-154">*는 필수 필드를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-154">An * means required field.</span></span>

| <span data-ttu-id="ad5ac-155">표시 이름</span><span class="sxs-lookup"><span data-stu-id="ad5ac-155">Display Name</span></span> | <span data-ttu-id="ad5ac-156">속성 이름</span><span class="sxs-lookup"><span data-stu-id="ad5ac-156">Property Name</span></span> | <span data-ttu-id="ad5ac-157">설명</span><span class="sxs-lookup"><span data-stu-id="ad5ac-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad5ac-158">구독 메서드*</span><span class="sxs-lookup"><span data-stu-id="ad5ac-158">Subscribe Method*</span></span> |<span data-ttu-id="ad5ac-159">메서드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-159">method</span></span> |<span data-ttu-id="ad5ac-160">구독 요청에 사용할 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-160">HTTP Method to use for subscribe request</span></span> |
| <span data-ttu-id="ad5ac-161">구독 URI*</span><span class="sxs-lookup"><span data-stu-id="ad5ac-161">Subscribe URI*</span></span> |<span data-ttu-id="ad5ac-162">uri</span><span class="sxs-lookup"><span data-stu-id="ad5ac-162">uri</span></span> |<span data-ttu-id="ad5ac-163">구독 요청에 사용할 HTTP URI</span><span class="sxs-lookup"><span data-stu-id="ad5ac-163">HTTP URI to use for subscribe request</span></span> |
| <span data-ttu-id="ad5ac-164">구독 취소 메서드*</span><span class="sxs-lookup"><span data-stu-id="ad5ac-164">Unsubscribe Method*</span></span> |<span data-ttu-id="ad5ac-165">메서드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-165">method</span></span> |<span data-ttu-id="ad5ac-166">구독 취소 요청에 사용할 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-166">HTTP method to use for unsubscribe request</span></span> |
| <span data-ttu-id="ad5ac-167">구독 취소 URI*</span><span class="sxs-lookup"><span data-stu-id="ad5ac-167">Unsubscribe URI*</span></span> |<span data-ttu-id="ad5ac-168">uri</span><span class="sxs-lookup"><span data-stu-id="ad5ac-168">uri</span></span> |<span data-ttu-id="ad5ac-169">구독 취소 요청에 사용할 HTTP URI</span><span class="sxs-lookup"><span data-stu-id="ad5ac-169">HTTP URI to use for unsubscribe request</span></span> |
| <span data-ttu-id="ad5ac-170">구독 본문</span><span class="sxs-lookup"><span data-stu-id="ad5ac-170">Subscribe Body</span></span> |<span data-ttu-id="ad5ac-171">body</span><span class="sxs-lookup"><span data-stu-id="ad5ac-171">body</span></span> |<span data-ttu-id="ad5ac-172">구독의 HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="ad5ac-172">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="ad5ac-173">구독 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-173">Subscribe Headers</span></span> |<span data-ttu-id="ad5ac-174">headers</span><span class="sxs-lookup"><span data-stu-id="ad5ac-174">headers</span></span> |<span data-ttu-id="ad5ac-175">구독의 HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-175">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="ad5ac-176">구독 인증</span><span class="sxs-lookup"><span data-stu-id="ad5ac-176">Subscribe Authentication</span></span> |<span data-ttu-id="ad5ac-177">authentication</span><span class="sxs-lookup"><span data-stu-id="ad5ac-177">authentication</span></span> |<span data-ttu-id="ad5ac-178">구독에 사용할 HTTP 인증</span><span class="sxs-lookup"><span data-stu-id="ad5ac-178">HTTP authentication to use for subscribe.</span></span> <span data-ttu-id="ad5ac-179">자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-179">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="ad5ac-180">구독 취소 본문</span><span class="sxs-lookup"><span data-stu-id="ad5ac-180">Unsubscribe Body</span></span> |<span data-ttu-id="ad5ac-181">body</span><span class="sxs-lookup"><span data-stu-id="ad5ac-181">body</span></span> |<span data-ttu-id="ad5ac-182">구독 취소의 HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="ad5ac-182">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="ad5ac-183">구독 취소 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-183">Unsubscribe Headers</span></span> |<span data-ttu-id="ad5ac-184">headers</span><span class="sxs-lookup"><span data-stu-id="ad5ac-184">headers</span></span> |<span data-ttu-id="ad5ac-185">구독 취소의 HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-185">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="ad5ac-186">구독 취소 인증</span><span class="sxs-lookup"><span data-stu-id="ad5ac-186">Unsubscribe Authentication</span></span> |<span data-ttu-id="ad5ac-187">authentication</span><span class="sxs-lookup"><span data-stu-id="ad5ac-187">authentication</span></span> |<span data-ttu-id="ad5ac-188">구독 취소에 사용할 HTTP 인증</span><span class="sxs-lookup"><span data-stu-id="ad5ac-188">HTTP authentication to use for unsubscribe.</span></span> <span data-ttu-id="ad5ac-189">자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-189">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="ad5ac-190">**출력 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="ad5ac-190">**Output Details**</span></span>

<span data-ttu-id="ad5ac-191">웹후크 요청</span><span class="sxs-lookup"><span data-stu-id="ad5ac-191">Webhook request</span></span>

| <span data-ttu-id="ad5ac-192">속성 이름</span><span class="sxs-lookup"><span data-stu-id="ad5ac-192">Property Name</span></span> | <span data-ttu-id="ad5ac-193">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="ad5ac-193">Data Type</span></span> | <span data-ttu-id="ad5ac-194">설명</span><span class="sxs-lookup"><span data-stu-id="ad5ac-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad5ac-195">headers</span><span class="sxs-lookup"><span data-stu-id="ad5ac-195">Headers</span></span> |<span data-ttu-id="ad5ac-196">object</span><span class="sxs-lookup"><span data-stu-id="ad5ac-196">object</span></span> |<span data-ttu-id="ad5ac-197">웹후크 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-197">Webhook request headers</span></span> |
| <span data-ttu-id="ad5ac-198">body</span><span class="sxs-lookup"><span data-stu-id="ad5ac-198">Body</span></span> |<span data-ttu-id="ad5ac-199">object</span><span class="sxs-lookup"><span data-stu-id="ad5ac-199">object</span></span> |<span data-ttu-id="ad5ac-200">웹후크 요청 개체</span><span class="sxs-lookup"><span data-stu-id="ad5ac-200">Webhook request object</span></span> |
| <span data-ttu-id="ad5ac-201">상태 코드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-201">Status Code</span></span> |<span data-ttu-id="ad5ac-202">int</span><span class="sxs-lookup"><span data-stu-id="ad5ac-202">int</span></span> |<span data-ttu-id="ad5ac-203">웹후크 요청 상태 코드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-203">Webhook request status code</span></span> |

## <a name="webhook-actions"></a><span data-ttu-id="ad5ac-204">웹후크 작업</span><span class="sxs-lookup"><span data-stu-id="ad5ac-204">Webhook actions</span></span>

| <span data-ttu-id="ad5ac-205">작업</span><span class="sxs-lookup"><span data-stu-id="ad5ac-205">Action</span></span> | <span data-ttu-id="ad5ac-206">설명</span><span class="sxs-lookup"><span data-stu-id="ad5ac-206">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad5ac-207">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="ad5ac-207">HTTP Webhook</span></span> |<span data-ttu-id="ad5ac-208">필요에 따라 URL을 호출할 수 있는 서비스에 대한 콜백 URL을 구독하여 워크플로 단계를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-208">Subscribe a callback URL to a service that can call the URL to resume a workflow step as needed.</span></span> |

### <a name="action-details"></a><span data-ttu-id="ad5ac-209">작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ad5ac-209">Action details</span></span>

#### <a name="http-webhook"></a><span data-ttu-id="ad5ac-210">HTTP 웹후크</span><span class="sxs-lookup"><span data-stu-id="ad5ac-210">HTTP Webhook</span></span>

<span data-ttu-id="ad5ac-211">필요에 따라 URL을 호출할 수 있는 서비스에 대한 콜백 URL을 구독하여 워크플로 단계를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-211">Subscribe a callback URL to a service that can call the URL to resume a workflow step as needed.</span></span>
<span data-ttu-id="ad5ac-212">*는 필수 필드를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-212">An * means required field.</span></span>

| <span data-ttu-id="ad5ac-213">표시 이름</span><span class="sxs-lookup"><span data-stu-id="ad5ac-213">Display Name</span></span> | <span data-ttu-id="ad5ac-214">속성 이름</span><span class="sxs-lookup"><span data-stu-id="ad5ac-214">Property Name</span></span> | <span data-ttu-id="ad5ac-215">설명</span><span class="sxs-lookup"><span data-stu-id="ad5ac-215">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad5ac-216">구독 메서드*</span><span class="sxs-lookup"><span data-stu-id="ad5ac-216">Subscribe Method*</span></span> |<span data-ttu-id="ad5ac-217">메서드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-217">method</span></span> |<span data-ttu-id="ad5ac-218">구독 요청에 사용할 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-218">HTTP Method to use for subscribe request</span></span> |
| <span data-ttu-id="ad5ac-219">구독 URI*</span><span class="sxs-lookup"><span data-stu-id="ad5ac-219">Subscribe URI*</span></span> |<span data-ttu-id="ad5ac-220">uri</span><span class="sxs-lookup"><span data-stu-id="ad5ac-220">uri</span></span> |<span data-ttu-id="ad5ac-221">구독 요청에 사용할 HTTP URI</span><span class="sxs-lookup"><span data-stu-id="ad5ac-221">HTTP URI to use for subscribe request</span></span> |
| <span data-ttu-id="ad5ac-222">구독 취소 메서드*</span><span class="sxs-lookup"><span data-stu-id="ad5ac-222">Unsubscribe Method*</span></span> |<span data-ttu-id="ad5ac-223">메서드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-223">method</span></span> |<span data-ttu-id="ad5ac-224">구독 취소 요청에 사용할 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-224">HTTP method to use for unsubscribe request</span></span> |
| <span data-ttu-id="ad5ac-225">구독 취소 URI*</span><span class="sxs-lookup"><span data-stu-id="ad5ac-225">Unsubscribe URI*</span></span> |<span data-ttu-id="ad5ac-226">uri</span><span class="sxs-lookup"><span data-stu-id="ad5ac-226">uri</span></span> |<span data-ttu-id="ad5ac-227">구독 취소 요청에 사용할 HTTP URI</span><span class="sxs-lookup"><span data-stu-id="ad5ac-227">HTTP URI to use for unsubscribe request</span></span> |
| <span data-ttu-id="ad5ac-228">구독 본문</span><span class="sxs-lookup"><span data-stu-id="ad5ac-228">Subscribe Body</span></span> |<span data-ttu-id="ad5ac-229">body</span><span class="sxs-lookup"><span data-stu-id="ad5ac-229">body</span></span> |<span data-ttu-id="ad5ac-230">구독의 HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="ad5ac-230">HTTP request body for subscribe</span></span> |
| <span data-ttu-id="ad5ac-231">구독 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-231">Subscribe Headers</span></span> |<span data-ttu-id="ad5ac-232">headers</span><span class="sxs-lookup"><span data-stu-id="ad5ac-232">headers</span></span> |<span data-ttu-id="ad5ac-233">구독의 HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-233">HTTP request headers for subscribe</span></span> |
| <span data-ttu-id="ad5ac-234">구독 인증</span><span class="sxs-lookup"><span data-stu-id="ad5ac-234">Subscribe Authentication</span></span> |<span data-ttu-id="ad5ac-235">authentication</span><span class="sxs-lookup"><span data-stu-id="ad5ac-235">authentication</span></span> |<span data-ttu-id="ad5ac-236">구독에 사용할 HTTP 인증</span><span class="sxs-lookup"><span data-stu-id="ad5ac-236">HTTP authentication to use for subscribe.</span></span> <span data-ttu-id="ad5ac-237">자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-237">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |
| <span data-ttu-id="ad5ac-238">구독 취소 본문</span><span class="sxs-lookup"><span data-stu-id="ad5ac-238">Unsubscribe Body</span></span> |<span data-ttu-id="ad5ac-239">body</span><span class="sxs-lookup"><span data-stu-id="ad5ac-239">body</span></span> |<span data-ttu-id="ad5ac-240">구독 취소의 HTTP 요청 본문</span><span class="sxs-lookup"><span data-stu-id="ad5ac-240">HTTP request body for unsubscribe</span></span> |
| <span data-ttu-id="ad5ac-241">구독 취소 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-241">Unsubscribe Headers</span></span> |<span data-ttu-id="ad5ac-242">headers</span><span class="sxs-lookup"><span data-stu-id="ad5ac-242">headers</span></span> |<span data-ttu-id="ad5ac-243">구독 취소의 HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-243">HTTP request headers for unsubscribe</span></span> |
| <span data-ttu-id="ad5ac-244">구독 취소 인증</span><span class="sxs-lookup"><span data-stu-id="ad5ac-244">Unsubscribe Authentication</span></span> |<span data-ttu-id="ad5ac-245">authentication</span><span class="sxs-lookup"><span data-stu-id="ad5ac-245">authentication</span></span> |<span data-ttu-id="ad5ac-246">구독 취소에 사용할 HTTP 인증</span><span class="sxs-lookup"><span data-stu-id="ad5ac-246">HTTP authentication to use for unsubscribe.</span></span> <span data-ttu-id="ad5ac-247">자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요.</span><span class="sxs-lookup"><span data-stu-id="ad5ac-247">[See HTTP connector](connectors-native-http.md#authentication) for details</span></span> |

<span data-ttu-id="ad5ac-248">**출력 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="ad5ac-248">**Output Details**</span></span>

<span data-ttu-id="ad5ac-249">웹후크 요청</span><span class="sxs-lookup"><span data-stu-id="ad5ac-249">Webhook request</span></span>

| <span data-ttu-id="ad5ac-250">속성 이름</span><span class="sxs-lookup"><span data-stu-id="ad5ac-250">Property Name</span></span> | <span data-ttu-id="ad5ac-251">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="ad5ac-251">Data Type</span></span> | <span data-ttu-id="ad5ac-252">설명</span><span class="sxs-lookup"><span data-stu-id="ad5ac-252">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad5ac-253">headers</span><span class="sxs-lookup"><span data-stu-id="ad5ac-253">Headers</span></span> |<span data-ttu-id="ad5ac-254">object</span><span class="sxs-lookup"><span data-stu-id="ad5ac-254">object</span></span> |<span data-ttu-id="ad5ac-255">웹후크 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="ad5ac-255">Webhook request headers</span></span> |
| <span data-ttu-id="ad5ac-256">body</span><span class="sxs-lookup"><span data-stu-id="ad5ac-256">Body</span></span> |<span data-ttu-id="ad5ac-257">object</span><span class="sxs-lookup"><span data-stu-id="ad5ac-257">object</span></span> |<span data-ttu-id="ad5ac-258">웹후크 요청 개체</span><span class="sxs-lookup"><span data-stu-id="ad5ac-258">Webhook request object</span></span> |
| <span data-ttu-id="ad5ac-259">상태 코드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-259">Status Code</span></span> |<span data-ttu-id="ad5ac-260">int</span><span class="sxs-lookup"><span data-stu-id="ad5ac-260">int</span></span> |<span data-ttu-id="ad5ac-261">웹후크 요청 상태 코드</span><span class="sxs-lookup"><span data-stu-id="ad5ac-261">Webhook request status code</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad5ac-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad5ac-262">Next steps</span></span>

* [<span data-ttu-id="ad5ac-263">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ad5ac-263">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="ad5ac-264">다른 커넥터 찾기</span><span class="sxs-lookup"><span data-stu-id="ad5ac-264">Find other connectors</span></span>](apis-list.md)