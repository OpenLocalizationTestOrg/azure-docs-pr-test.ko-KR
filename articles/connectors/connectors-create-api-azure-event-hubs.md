---
title: "Azure Logic Apps용 Azure Event Hubs로 이벤트 모니터 설정 | Microsoft Docs"
description: "Azure Event Hubs로 Azure Logic Apps에 대한 이벤트를 수신 및 전송하는 데이터 스트림 모니터"
services: logic-apps
keywords: "데이터 스트림, 이벤트 모니터, 이벤트 허브"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 2ca27fb8269d1796fb1181fc4d0a8744a592d548
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="4e540-104">Event Hubs 커넥터로 이벤트 모니터, 수신 및 전송</span><span class="sxs-lookup"><span data-stu-id="4e540-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="4e540-105">논리 앱이 이벤트를 감지하고 이벤트를 수신 및 전송할 수 있도록 이벤트 모니터를 설정하려면 논리 앱에서 [Azure Event Hub](https://azure.microsoft.com/services/event-hubs)에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="4e540-106">[Azure 이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="4e540-107">요구 사항</span><span class="sxs-lookup"><span data-stu-id="4e540-107">Requirements</span></span>

* <span data-ttu-id="4e540-108">Azure에 [Event Hubs 네임스페이스 및 Event Hub](../event-hubs/event-hubs-create.md)가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="4e540-109">[Event Hubs 네임스페이스 및 Event Hub를 만드는 방법](../event-hubs/event-hubs-create.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4e540-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="4e540-110">논리 앱에서 [커넥터](https://docs.microsoft.com/azure/connectors/apis-list)를 사용하려면 먼저 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="4e540-111">[논리 앱을 만드는 방법](../logic-apps/logic-apps-create-a-logic-app.md)을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4e540-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="4e540-112">Event Hubs 네임스페이스 권한 확인 및 연결 문자열 찾기</span><span class="sxs-lookup"><span data-stu-id="4e540-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="4e540-113">논리 앱에서 모든 서비스에 액세스하려면 논리 앱과 서비스 사이에 [*연결*](./connectors-overview.md)을 만들어야 합니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="4e540-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="4e540-114">이렇게 연결되면 논리 앱에서 데이터에 액세스할 수 있는 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="4e540-115">Event Hub에 액세스하는 논리 앱의 경우 Event Hubs 네임스페이스에 대한 **관리** 권한과 연결 문자열이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="4e540-116">사용 권한을 확인하고 연결 문자열을 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="4e540-117">[Azure Portal](https://portal.azure.com "Azure Portal")에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="4e540-118">특정 Event Hub가 아닌 Event Hubs *네임스페이스*로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="4e540-119">네임스페이스 블레이드의 **설정** 아래에서 **공유 액세스 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="4e540-120">**클레임** 아래에서 해당 네임스페이스에 대한 **관리** 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Event Hub 네임스페이스에 대한 관리 권한](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="4e540-122">Event Hubs 네임스페이스에 대한 연결 문자열을 복사하려면 **RootManageSharedAccessKey**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="4e540-123">기본 키 연결 문자열 옆에 있는 복사 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![Event Hubs 네임스페이스 연결 문자열 복사](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="4e540-125">연결 문자열이 Event Hubs 네임스페이스 또는 특정 Event Hub와 연결되어 있는지 확인하려면 `EntityPath` 매개 변수에 대한 연결 문자열을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="4e540-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="4e540-126">이 매개 변수를 찾으면 연결 문자열은 특정 Event Hub “엔터티”에 대한 것이고 논리 앱에 사용할 올바른 문자열이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="4e540-127">이제 Event Hubs 트리거 또는 작업을 논리 앱에 추가한 후 자격 증명을 묻는 메시지가 표시되면 Event Hubs 네임스페이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="4e540-128">연결에 이름을 지정하고 복사한 연결 문자열을 입력하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![Event Hubs 네임스페이스에 대한 연결 문자열 입력](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="4e540-130">연결을 만들면 연결 이름이 Event Hubs 트리거 또는 작업에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="4e540-131">그런 다음 논리 앱에서 다른 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-131">You can then continue with the other steps in your logic app.</span></span>

    ![Event Hubs 네임스페이스 연결 생성됨](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="4e540-133">Event Hub에서 새 이벤트를 수신하면 워크플로 시작</span><span class="sxs-lookup"><span data-stu-id="4e540-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="4e540-134">[*트리거*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)는 논리 앱에서 워크플로를 시작하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="4e540-135">새 이벤트가 Event Hub에 전송되었을 때 워크플로를 시작하려면 이 이벤트를 감지하는 트리거를 추가하는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="4e540-136">[Azure Portal](https://portal.azure.com "Azure Portal")에서 기존 논리 앱으로 이동하거나 비어 있는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="4e540-137">논리 앱 디자이너의 검색 상자에 필터에 대한 `event hubs`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="4e540-138">이 트리거 선택: **이벤트가 Event Hub에서 사용 가능한 경우**</span><span class="sxs-lookup"><span data-stu-id="4e540-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Event Hub에서 새 이벤트를 수신하는 경우에 대한 트리거 선택](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="4e540-140">Event Hubs 네임스페이스에 대한 연결이 아직 없는 경우 이 연결을 생성할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="4e540-141">연결에 이름을 지정하고 Event Hubs 네임스페이스에 대한 연결 문자열을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="4e540-142">필요한 경우 [연결 문자열을 찾는 방법](#permissions-connection-string)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4e540-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![Event Hubs 네임스페이스에 대한 연결 문자열 입력](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="4e540-144">연결을 생성한 후에는 **이벤트가 Event Hub에서 사용 가능한 경우** 트리거에 대한 설정이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Event Hub에서 새 이벤트를 수신하는 경우에 대한 트리거 설정](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="4e540-146">모니터할 Event Hub에 대한 이름을 입력 또는 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="4e540-147">Event Hub를 얼마나 자주 확인할지 빈도와 간격을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="4e540-148">필요할 경우 이벤트를 읽기 위한 소비자 그룹을 선택하고 **고급 옵션 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Event Hub 또는 소비자 그룹 지정](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="4e540-150">이제 논리 앱에 대한 워크플로를 시작할 트리거를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="4e540-151">논리 앱에서 설정한 일정에 따라 지정된 Event Hub를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="4e540-152">앱이 Event Hub에서 새 이벤트를 찾으면 트리거가 논리 앱의 다른 작업 또는 트리거를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="4e540-153">논리 앱에서 Event Hub로 이벤트 보내기</span><span class="sxs-lookup"><span data-stu-id="4e540-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="4e540-154">[*작업*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)은 논리 앱 워크플로에서 수행하는 태스크입니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="4e540-155">논리 앱에 트리거를 추가한 후에 해당 트리거에 의해 생성된 데이터를 사용하여 작업을 수행하는 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="4e540-156">논리 앱에서 Event Hub로 이벤트를 보내려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="4e540-157">논리 앱 디자이너의 논리 앱 트리거 아래에서 **새 단계** > **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![[새 단계]를 선택한 후 [작업 추가]를 선택합니다.](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="4e540-159">이제 수행할 작업을 찾아 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="4e540-160">어떤 작업이라도 선택할 수 있지만 이 예에서는 이벤트를 보내는 Event Hubs 작업을 선택하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="4e540-161">검색 상자에서 필터에 `event hubs`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="4e540-162">이 작업 선택: **이벤트 보내기**</span><span class="sxs-lookup"><span data-stu-id="4e540-162">Select this action: **Send event**</span></span>

    ![[Event Hubs - 이벤트 보내기] 작업을 선택합니다.](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="4e540-164">이벤트에 필요한 정보(예: 이벤트를 보낼 Event Hub 이름)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="4e540-165">이벤트에 대한 다른 선택적 정보(예: 이벤트에 대한 콘텐츠)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="4e540-166">이벤트를 보낼 Event Hub 파티션을 필요에 따라 지정하려면 **고급 옵션 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![Event Hub 이름 및 선택적 이벤트 정보 입력](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="4e540-168">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-168">Save your changes.</span></span>

    ![논리 앱 저장](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="4e540-170">이제 논리 앱에서 이벤트를 보내는 작업을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="4e540-171">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="4e540-171">Connector-specific details</span></span>

<span data-ttu-id="4e540-172">[커넥터 세부 정보](/connectors/eventhubs/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e540-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="4e540-173">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="4e540-173">Get help</span></span>

<span data-ttu-id="4e540-174">질문하고, 질문에 답변하고, 다른 Azure Logic Apps 사용자가 어떤 일을 하는지 확인하려면 [Azure Logic Apps 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="4e540-174">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="4e540-175">Logic Apps 및 커넥터 개선에 도움을 주려면 [Logic Apps 사용자 의견 사이트](http://aka.ms/logicapps-wish)에서 투표하고 아이디어를 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="4e540-175">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e540-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e540-176">Next steps</span></span>

*  [<span data-ttu-id="4e540-177">Azure Logic Apps용 다른 커넥터 찾기</span><span class="sxs-lookup"><span data-stu-id="4e540-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)