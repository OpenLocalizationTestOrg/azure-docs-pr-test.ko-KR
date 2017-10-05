---
title: "논리 앱에서 Office 365 Outlook 커넥터 추가 | Microsoft Docs"
description: "Office 365와 상호 작용할 수 있도록 Office 365 커넥터로 논리 앱을 만듭니다. 예: 연락처 및 일정 항목 만들기, 편집 및 업데이트."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 5335dae62e61659b68e8befb4ed0d404dffb800c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-outlook-connector"></a><span data-ttu-id="419de-104">Office 365 Outlook 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="419de-104">Get started with the Office 365 Outlook connector</span></span>
<span data-ttu-id="419de-105">Office 365 Outlook 커넥터를 통해 Office 365에서 Outlook과 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="419de-105">The Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="419de-106">이 커넥터를 사용하여 연락처 및 일정 항목을 만들기, 편집 및 업데이트하고 전자 메일을 가져오고 보내며 회신할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="419de-106">Use this connector to create, edit, and update contacts and calendar items, and also get, send, and reply to email.</span></span>

<span data-ttu-id="419de-107">Office 365 Outlook을 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="419de-108">Office 365 내에서 전자 메일 및 일정 기능을 사용하여 워크플로를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-108">Build your workflow using the email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="419de-109">새 전자 메일이 있거나 일정 항목이 업데이트될 때 트리거를 사용하여 워크플로를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-109">Use triggers to start your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="419de-110">전자 메일을 보내고 새 일정 이벤트를 만드는 등의 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-110">Use actions to send an email, create a new calendar event, and more.</span></span> <span data-ttu-id="419de-111">예를 들어 Salesforce에 새 개체(트리거)가 있는 경우 Office 365 Outlook으로 전자 메일을 보냅니다(작업).</span><span class="sxs-lookup"><span data-stu-id="419de-111">For example, when there is a new object in Salesforce (a trigger), send an email to your Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="419de-112">이 항목에서는 논리 앱에서 Office 365 Outlook 커넥터를 사용하는 방법을 보여 주고, 트리거 및 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-112">This topic shows you how to use the Office 365 Outlook connector in a logic app, and also lists the triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="419de-113">이 버전의 문서는 논리 앱 GA(일반 공급)에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="419de-113">This version of the article applies to Logic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="419de-114">Logic Apps에 대해 자세히 알아보려면 [논리 앱이란 무엇인가요?](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="419de-114">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="419de-115">Office 365에 연결</span><span class="sxs-lookup"><span data-stu-id="419de-115">Connect to Office 365</span></span>
<span data-ttu-id="419de-116">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-116">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="419de-117">연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="419de-118">예를 들어 Office 365 Outlook에 연결하려면 먼저 Office 365 *연결*이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-118">For example, to connect to Office 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="419de-119">연결을 만들려면 연결하려는 서비스에 액세스할 때 일반적으로 사용하는 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-119">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="419de-120">따라서 Office 365 Outlook을 사용하는 경우 Office 365 계정에 대한 자격 증명을 입력하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="419de-120">So with Office 365 Outlook, enter the credentials to your Office 365 account to create the connection.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="419de-121">연결 만들기</span><span class="sxs-lookup"><span data-stu-id="419de-121">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to Office 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="419de-122">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="419de-122">Use a trigger</span></span>
<span data-ttu-id="419de-123">트리거는 논리 앱에 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="419de-123">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="419de-124">원하는 간격 및 빈도로 서비스의 "폴링"을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-124">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="419de-125">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="419de-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="419de-126">논리 앱에서 트리거 목록을 가져오려면 "office 365"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-126">In the logic app, type "office 365" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="419de-127">**Office 365 Outlook - 예정된 이벤트가 곧 시작될 때**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="419de-128">연결이 이미 있는 경우 드롭다운 목록에서 일정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-128">If a connection already exists, then select a calendar from the drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="419de-129">로그인하라는 메시지가 표시되면 로그인 세부 정보를 입력하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="419de-129">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="419de-130">이 항목의 [연결 만들기](connectors-create-api-office365-outlook.md#create-the-connection)에서 단계가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="419de-130">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="419de-131">이 예제에서는 일정 이벤트가 업데이트되면 논리 앱이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="419de-131">In this example, the logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="419de-132">이 트리거의 결과를 보려면 텍스트 메시지를 보내는 다른 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-132">To see the results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="419de-133">예를 들어 일정 이벤트가 15분 내에 시작되는 경우 텍스트를 보내는 Twilio *메시지 보내기* 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-133">For example, add the Twilio *Send message* action that texts you when the calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="419de-134">**편집** 단추를 선택하고 **빈도** 및 **간격** 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-134">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="419de-135">예를 들어 15분마다 폴링을 트리거하려면 **빈도**를 **분**으로, **간격**을 **15**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-135">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="419de-136">변경 내용을 **저장**합니다(도구 모음 왼쪽 위 모서리).</span><span class="sxs-lookup"><span data-stu-id="419de-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="419de-137">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="419de-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="419de-138">작업 사용</span><span class="sxs-lookup"><span data-stu-id="419de-138">Use an action</span></span>
<span data-ttu-id="419de-139">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="419de-139">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="419de-140">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="419de-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="419de-141">더하기 기호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-141">Select the plus sign.</span></span> <span data-ttu-id="419de-142">**작업 추가**, **조건 추가** 또는 **자세히** 옵션 중 하나 등 몇 가지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="419de-142">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="419de-143">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="419de-144">사용 가능한 모든 작업의 목록을 표시하려면 텍스트 상자에 "office 365"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-144">In the text box, type “office 365” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="419de-145">이 예제에서는 **Office 365 Outlook - 연락처 만들기**를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="419de-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="419de-146">연결이 이미 존재하는 경우 **폴더 ID**, **지정된 이름** 및 기타 속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-146">If a connection already exists, then choose the **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="419de-147">연결 정보를 묻는 메시지가 표시되면 연결을 만들기 위한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-147">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="419de-148">이 항목의 [연결 만들기](connectors-create-api-office365-outlook.md#create-the-connection)에서는 이러한 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-148">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="419de-149">이 예제에서는 Office 365 Outlook에 새 연락처를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="419de-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="419de-150">다른 트리거의 출력을 사용하여 연락처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="419de-150">You can use output from another trigger to create the contact.</span></span> <span data-ttu-id="419de-151">예를 들어 SalesForce *개체를 만들 때* 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-151">For example, add the SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="419de-152">그런 다음 SalesForce 필드를 사용하여 Office 365에서 새 연락처를 만드는 Office 365 Outlook *연락처 만들기* 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="419de-152">Then add the Office 365 Outlook *Create contact* action that uses the SalesForce fields to create the new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="419de-153">변경 내용을 **저장**합니다(도구 모음 왼쪽 위 모서리).</span><span class="sxs-lookup"><span data-stu-id="419de-153">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="419de-154">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="419de-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="419de-155">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="419de-155">Connector-specific details</span></span>

<span data-ttu-id="419de-156">[커넥터 세부 정보](/connectors/office365connector/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="419de-156">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="419de-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="419de-157">Next Steps</span></span>
<span data-ttu-id="419de-158">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="419de-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="419de-159">[API 목록](apis-list.md)에서 Logic Apps의 사용 가능한 다른 커넥터를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="419de-159">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

