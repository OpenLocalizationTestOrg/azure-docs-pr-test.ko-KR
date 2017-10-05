---
title: "그룹 또는 컬렉션으로 메시지를 일괄 처리 - Azure Logic Apps | Microsoft Docs"
description: "논리 앱에서의 일괄 처리에 대한 메시지 보내기 및 받기"
keywords: "일괄 처리"
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 480ffce5dbe7c25181bb0ba5639de884e98ff4e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="25bdd-104">논리 앱의 메시지 보내기, 받기 및 일괄 처리</span><span class="sxs-lookup"><span data-stu-id="25bdd-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="25bdd-105">그룹에서 함께 메시지를 처리하려면 데이터 항목 또는 메시지를 *일괄 처리*로 보내 해당 항목을 일괄 처리로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-105">To process messages together in groups, you can send data items, or messages, to a *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="25bdd-106">이 방법은 데이터 항목을 특정 방식으로 그룹화하여 함께 처리하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-106">This approach is useful when you want to make sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="25bdd-107">**일괄 처리** 트리거를 사용하여 항목을 일괄 처리로 수신하는 논리 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-107">You can create logic apps that receive items as a batch by using the **Batch** trigger.</span></span> <span data-ttu-id="25bdd-108">그런 다음 **Batch** 작업을 사용하여 항목을 일괄 처리로 보내는 논리 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-108">You can then create logic apps that send items to a batch by using the **Batch** action.</span></span>

<span data-ttu-id="25bdd-109">이 토픽에서는 이러한 작업을 수행하여 일괄 처리 솔루션을 빌드할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="25bdd-110">[항목을 일괄 처리로 수신하고 수집하는 논리 앱을 만듭니다](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="25bdd-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="25bdd-111">이 “일괄 처리 수신자” 논리 앱은 수신자 논리 앱을 해제하고 항목을 처리하기 전에 충족해야 하는 일괄 처리 이름 및 릴리스 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-111">This "batch receiver" logic app specifies the batch name and release criteria to meet before the receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="25bdd-112">[항목을 일괄 처리로 보내는 논리 앱을 만듭니다](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="25bdd-112">[Create a logic app that sends items to a batch](#batch-sender).</span></span> <span data-ttu-id="25bdd-113">이 “일괄 처리 발신자” 논리 앱은 기존 일괄 처리 수신자 논리 앱이어야 하는 항목을 보낼 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-113">This "batch sender" logic app specifies where to send items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="25bdd-114">또한 사용자 지정 번호와 같이 고유한 키를 지정하여 대상 일괄 처리를 해당 키에 따라 하위 집합으로 “분할”하거나 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-114">You can also specify a unique key, like a customer number, to "partition", or divide, the target batch into subsets based on that key.</span></span> <span data-ttu-id="25bdd-115">이런 방식으로 해당 키가 있는 모든 항목이 함께 수집되어 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="25bdd-116">요구 사항</span><span class="sxs-lookup"><span data-stu-id="25bdd-116">Requirements</span></span>

<span data-ttu-id="25bdd-117">이 예제를 수행하려면 다음과 같은 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-117">To follow this example, you need these items:</span></span>

* <span data-ttu-id="25bdd-118">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="25bdd-118">An Azure subscription.</span></span> <span data-ttu-id="25bdd-119">구독이 없는 경우 [Azure 계정을 사용하여 시작](https://azure.microsoft.com/free/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="25bdd-120">그렇지 않으면 [종량제 구독에 등록](https://azure.microsoft.com/pricing/purchase-options/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="25bdd-121">[논리 앱 만드는 방법](../logic-apps/logic-apps-create-a-logic-app.md)에 관한 기본 지식</span><span class="sxs-lookup"><span data-stu-id="25bdd-121">Basic knowledge about [how to create logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="25bdd-122">[Azure Logic Apps에서 지원하는 전자 메일 공급자](../connectors/apis-list.md)를 사용하는 메일 계정</span><span class="sxs-lookup"><span data-stu-id="25bdd-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="25bdd-123">메시지를 일괄 처리로 수신하는 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="25bdd-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="25bdd-124">메시지를 일괄 처리로 보내려면 **일괄 처리** 트리거를 사용하여 “일괄 처리 수신자” 논리 앱을 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-124">Before you can send messages to a batch, you must first create a "batch receiver" logic app with the **Batch** trigger.</span></span> <span data-ttu-id="25bdd-125">이런 방식으로 발신자 논리 앱을 만들 때 이 수신자 논리 앱을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-125">That way, you can select this receiver logic app when you create the sender logic app.</span></span> <span data-ttu-id="25bdd-126">수신자의 경우 일괄 처리 이름, 릴리스 조건 및 다른 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-126">For the receiver, you specify the batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="25bdd-127">수신자 논리 앱은 발신자에 대해 알 필요가 없는 반면, 발신자 논리 앱은 항목을 보내는 곳을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-127">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="25bdd-128">[Azure Portal](https://portal.azure.com)에서 “BatchReceiver”라는 이름을 가진 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-128">In the [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="25bdd-129">Logic Apps 디자이너에서 논리 앱 워크플로를 시작하는 **Batch** 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-129">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="25bdd-130">검색 상자에서 필터로 “일괄 처리”를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-130">In the search box, enter "batch" as your filter.</span></span> <span data-ttu-id="25bdd-131">**Batch – Batch 메시지** 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Batch 트리거 추가](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="25bdd-133">일괄 처리에 사용할 이름을 입력하고, 다음 예와 같이 일괄 처리를 릴리스하기 위한 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-133">Provide a name for the batch, and specify criteria for releasing the batch, for example:</span></span>

   * <span data-ttu-id="25bdd-134">**일괄 처리 이름**: 일괄 처리를 식별하는 데 사용되는 이름으로, 이 예제에서는 “TestBatch”입니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-134">**Batch Name**: The name used to identify the batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="25bdd-135">**메시지 수**: 처리를 릴리스하기 전 일괄 처리로 저장하는 메시지 수입니다. 이 예제에서는 “5”입니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-135">**Message Count**: The number of messages to hold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Batch 트리거 세부 정보 제공](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="25bdd-137">일괄 처리 트리거가 발생할 때 전자 메일을 보내는 다른 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-137">Add another action that sends an email when the batch trigger fires.</span></span> <span data-ttu-id="25bdd-138">일괄 처리에 항목이 5개가 될 때마다 논리 앱에서 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-138">Each time the batch has five items, the logic app sends an email.</span></span>

   1. <span data-ttu-id="25bdd-139">일괄 처리 트리거에서 **+다음 단계** > **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-139">Under the batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="25bdd-140">검색 상자에서 필터로 “전자 메일”을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-140">In the search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="25bdd-141">전자 메일 공급자에 따라 전자 메일 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="25bdd-142">예를 들어 회사 또는 학교 계정이 있는 경우 Office 365 Outlook 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-142">For example, if you have a work or school account, select the Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="25bdd-143">Gmail 계정이 있는 경우 Gmail 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-143">If you have a Gmail account, select the Gmail connector.</span></span>

   3. <span data-ttu-id="25bdd-144">커넥터에 대해 **{*전자 메일 공급자*} - 전자 메일 보내기** 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="25bdd-145">예:</span><span class="sxs-lookup"><span data-stu-id="25bdd-145">For example:</span></span>

      ![전자 메일 공급자에 대한 “전자 메일 보내기” 작업을 선택합니다.](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="25bdd-147">이전에 전자 메일 공급자에 대한 연결을 만들지 않은 경우 메시지가 표시되면 인증을 위해 전자 메일 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="25bdd-148">[전자 메일 자격 증명 인증](../logic-apps/logic-apps-create-a-logic-app.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="25bdd-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="25bdd-149">방금 추가한 작업에 대한 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-149">Set the properties for the action you just added.</span></span>

   * <span data-ttu-id="25bdd-150">**받는 사람** 상자에 받는 사람의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-150">In the **To** box, enter the recipient's email address.</span></span> 
   <span data-ttu-id="25bdd-151">자신의 이메일 주소를 사용하여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="25bdd-152">**제목** 상자에 **동적 콘텐츠** 목록이 표시되면 **파티션 이름** 필드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-152">In the **Subject** box, when the **Dynamic content** list appears, select the **Partition Name** field.</span></span>

     ![“동적 콘텐츠” 목록에서 “파티션 이름”을 선택합니다.](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="25bdd-154">이후 섹션에서 메시지를 보낼 수 있는 논리적 집합으로 대상 일괄 처리를 분할하는 고유한 파티션 키를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-154">In a later section, you can specify a unique partition key that divides the target batch into logical sets to where you can send messages.</span></span> 
     <span data-ttu-id="25bdd-155">각 집합에는 발신자 논리 앱에서 생성된 고유 번호가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-155">Each set has a unique number that's generated by the sender logic app.</span></span> 
     <span data-ttu-id="25bdd-156">이 기능을 사용하면 여러 하위 집합이 있는 단일 일괄 처리를 사용하고 사용자가 제공한 이름으로 각 하위 집합을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-156">This capability lets you use a single batch with multiple subsets and define each subset with the name that you provide.</span></span>

   * <span data-ttu-id="25bdd-157">**본문** 상자에 **동적 콘텐츠** 목록이 표시되면 **메시지 ID** 필드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-157">In the **Body** box, when the **Dynamic content** list appears, select the **Message Id** field.</span></span>

     ![“본문”에서 “메시지 ID”를 선택합니다.](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="25bdd-159">전자 메일 보내기 작업에 대한 입력은 배열이므로 디자이너에서 자동으로 **각 항목** 루프를 **전자 메일 보내기** 작업에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-159">Because the input for the send email action is an array, the designer automatically adds a **For each** loop around the **Send an email** action.</span></span> 
     <span data-ttu-id="25bdd-160">이 루프는 일괄 처리의 각 항목에 대해 내부 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-160">This loop performs the inner action on each item in the batch.</span></span> 
     <span data-ttu-id="25bdd-161">따라서 5개 항목에 설정된 일괄 처리 트리거를 사용하면 트리거가 발생할 때마다 5개의 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-161">So, with the batch trigger set to five items, you get five emails each time the trigger fires.</span></span>

7.  <span data-ttu-id="25bdd-162">이제 일괄 처리 수신기 논리 앱을 만들었으므로 논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![논리 앱 저장](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-to-a-batch"></a><span data-ttu-id="25bdd-164">일괄 처리로 메시지를 보내는 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="25bdd-164">Create logic apps that send messages to a batch</span></span>

<span data-ttu-id="25bdd-165">이제는 수신기 논리 앱에서 정의되는 일괄 처리로 항목을 보내는 논리 앱을 하나 이상 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-165">Now create one or more logic apps that send items to the batch defined by the receiver logic app.</span></span> <span data-ttu-id="25bdd-166">발신자의 경우 수신자 논리 앱 및 일괄 처리 이름, 메시지 콘텐츠 및 다른 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-166">For the sender, you specify the receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="25bdd-167">필요에 따라 해당 키가 있는 항목을 수집하도록 일괄 처리를 하위 집합으로 나누는 고유한 파티션 키를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-167">You can optionally provide a unique partition key to divide the batch into subsets to collect items with that key.</span></span>

<span data-ttu-id="25bdd-168">수신자 논리 앱은 발신자에 대해 알 필요가 없는 반면, 발신자 논리 앱은 항목을 보내는 곳을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-168">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="25bdd-169">“BatchSender”라는 이름을 가진 다른 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="25bdd-170">검색 상자에서 필터로 “되풀이”를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-170">In the search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="25bdd-171">**예약 - 되풀이** 트리거 선택</span><span class="sxs-lookup"><span data-stu-id="25bdd-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![“예약 - 되풀이” 트리거 추가](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="25bdd-173">1분마다 발신자 논리 앱을 실행하도록 빈도 및 간격을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-173">Set the frequency and interval to run the sender logic app every minute.</span></span>

      ![되풀이 트리거에 대한 빈도 및 간격 설정](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="25bdd-175">일괄 처리로 메시지를 보내기 위한 새 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-175">Add a new step for sending messages to a batch.</span></span>

   1. <span data-ttu-id="25bdd-176">되풀이 트리거에서 **+새 단계** > **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-176">Under the recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="25bdd-177">검색 상자에서 필터로 “일괄 처리”를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-177">In the search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="25bdd-178">**일괄 처리로 메시지 보내기 – 일괄 처리 트리거를 사용하여 논리 앱 워크플로 선택** 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-178">Select this action: **Send messages to batch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![“일괄 처리로 메시지 보내기” 선택](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="25bdd-180">이제 작업으로 표시되는 이전에 만든 “BatchReceiver” 논리 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![“일괄 처리 수신기” 논리 앱 선택](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="25bdd-182">목록에 일괄 처리 트리거가 있는 다른 논리 앱도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-182">The list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="25bdd-183">일괄 처리 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-183">Set the batch properties.</span></span>

   * <span data-ttu-id="25bdd-184">**일괄 처리 이름**: 수신기 논리 앱에서 정의되는 일괄 처리 이름입니다. 이 예에서는 “TestBatch”이며, 런타임에 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-184">**Batch Name**: The batch name defined by the receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="25bdd-185">일괄 처리 이름을 변경하지 않았는지 확인합니다. 이는 수신기 논리 앱에서 지정되는 일괄 처리 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-185">Make sure that you don't change the batch name, which must match the batch name that's specified by the receiver logic app.</span></span>
     > <span data-ttu-id="25bdd-186">일괄 처리 이름을 변경하면 발신자 논리 앱이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-186">Changing the batch name causes the sender logic app to fail.</span></span>

   * <span data-ttu-id="25bdd-187">**메시지 콘텐츠**: 보낼 메시지 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-187">**Message Content**: The message content that you want to send.</span></span> 
   <span data-ttu-id="25bdd-188">이 예제의 경우 현재 날짜 및 시간을 일괄 처리로 보내는 메시지 콘텐츠에 삽입하는 이 식을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-188">For this example, add this expression that inserts the current date and time into the message content that you send to the batch:</span></span>

     1. <span data-ttu-id="25bdd-189">**동적 콘텐츠** 목록이 표시되면 **식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-189">When the **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="25bdd-190">식 **utcnow()**를 입력하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-190">Enter the expression **utcnow()**, and choose **OK**.</span></span> 

        ![“메시지 콘텐츠”에서 “식”을 선택합니다.](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="25bdd-193">이제 일괄 처리에 대한 파티션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-193">Now set up a partition for the batch.</span></span> <span data-ttu-id="25bdd-194">“BatchReceiver” 작업에서 **고급 옵션 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-194">In the "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="25bdd-195">**파티션 이름**: 대상 일괄 처리를 나누는 데 사용하는 선택적 고유 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-195">**Partition Name**: An optional unique partition key to use for dividing the target batch.</span></span> <span data-ttu-id="25bdd-196">이 예제의 경우 1과 5 사이의 난수를 생성하는 식을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="25bdd-197">**동적 콘텐츠** 목록이 표시되면 **식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-197">When the **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="25bdd-198">**rand(1,6)** 식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-198">Enter this expression: **rand(1,6)**</span></span>

        ![대상 일괄 처리에 대한 파티션 설정](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="25bdd-200">이 **rand** 함수는 1과 5 사이의 숫자를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="25bdd-201">따라서 이 식이 동적으로 설정하는 번호가 지정된 5개 파티션으로 이 일괄 처리를 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="25bdd-202">**메시지 ID**: 선택적 메시지 식별자로, 비어 있는 경우 생성된 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="25bdd-203">이 예제의 경우 빈 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="25bdd-204">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-204">Save your logic app.</span></span> <span data-ttu-id="25bdd-205">발신자 논리 앱이 이제 다음 예제와 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-205">Your sender logic app now looks similar to this example:</span></span>

   ![발신자 논리 앱 저장](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="25bdd-207">논리 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="25bdd-207">Test your logic apps</span></span>

<span data-ttu-id="25bdd-208">일괄 처리 솔루션을 테스트하려면 논리 앱을 몇 분 동안 실행 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-208">To test your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="25bdd-209">곧 동일한 파티션 키를 사용하는 5개 그룹에서 전자 메일을 받기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-209">Soon, you start getting emails in groups of five, all with the same partition key.</span></span>

<span data-ttu-id="25bdd-210">BatchSender 논리 앱은 1분마다 실행되며, 1부터 5 사이의 난수를 생성하고, 메시지를 보내는 대상 일괄 처리에 대한 파티션 키로 이 생성된 번호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as the partition key for the target batch where messages are sent.</span></span> <span data-ttu-id="25bdd-211">일괄 처리에 동일한 파티션 키를 사용하는 5개 항목이 있을 때마다 BatchReceiver 논리 앱이 발생하고 각 메시지에 대한 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-211">Each time the batch has five items with the same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25bdd-212">테스트를 수행할 때 메시지를 보내지 않도록 BatchSender 논리 앱을 비활성화하여 받은 편지함이 오버로드되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="25bdd-212">When you're done testing, make sure that you disable the BatchSender logic app to stop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25bdd-213">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25bdd-213">Next steps</span></span>

* [<span data-ttu-id="25bdd-214">JSON을 사용하여 논리 앱 정의 빌드</span><span class="sxs-lookup"><span data-stu-id="25bdd-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="25bdd-215">Azure Logic Apps 및 함수를 사용하여 Visual Studio에서 서버를 사용하지 않는 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="25bdd-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="25bdd-216">논리 앱에 대한 예외 처리 및 오류 로깅</span><span class="sxs-lookup"><span data-stu-id="25bdd-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
