---
title: "논리 앱에 OneDrive 커넥터 추가 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 OneDrive 커넥터 개요"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 63bd33bf4e09b98aa53dcfec9fcc4a0109204952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="d73d7-103">OneDrive 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="d73d7-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="d73d7-104">OneDrive에 연결하여 파일 업로드, 가져오기, 삭제 등을 포함하여 파일을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="d73d7-105">OneDrive를 사용하여 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="d73d7-106">OneDrive에서 파일을 저장하여 워크플로를 작성하거나 OneDrive의 기존 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="d73d7-107">트리거를 사용하여 OneDrive 내에서 파일이 만들어지거나 업데이트될 때 워크플로를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="d73d7-108">파일 만들기, 파일 삭제 등의 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="d73d7-109">예를 들어 새 Office 365 전자 메일이 첨부 파일과 함께 수신되면(트리거) OneDrive에 새 파일을 만듭니다(작업).</span><span class="sxs-lookup"><span data-stu-id="d73d7-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="d73d7-110">이 토픽에서는 논리 앱에서 OneDrive 커넥터를 사용하는 방법을 보여 주고, 트리거 및 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="d73d7-111">Logic Apps에 대해 자세히 알아보려면 [논리 앱이란 무엇인가요?](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d73d7-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="d73d7-112">OneDrive에 연결</span><span class="sxs-lookup"><span data-stu-id="d73d7-112">Connect to OneDrive</span></span>
<span data-ttu-id="d73d7-113">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="d73d7-114">연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="d73d7-115">예를 들어 OneDrive에 연결하려면 먼저 OneDrive *연결*이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="d73d7-116">연결을 만들려면 연결하려는 서비스에 액세스할 때 일반적으로 사용하는 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="d73d7-117">따라서 OneDrive를 사용하는 경우 OneDrive 계정에 대한 자격 증명을 입력하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="d73d7-118">연결 만들기</span><span class="sxs-lookup"><span data-stu-id="d73d7-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="d73d7-119">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="d73d7-119">Use a trigger</span></span>
<span data-ttu-id="d73d7-120">트리거는 논리 앱에 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="d73d7-121">원하는 간격 및 빈도로 서비스의 "폴링"을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="d73d7-122">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="d73d7-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="d73d7-123">논리 앱에서 트리거 목록을 가져오려면 "onedrive"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="d73d7-124">**파일을 수정할 때**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-124">Select **When a file is modified**.</span></span> <span data-ttu-id="d73d7-125">연결이 이미 있는 경우 선택 표시 단추를 선택하여 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="d73d7-126">로그인하라는 메시지가 표시되면 로그인 세부 정보를 입력하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="d73d7-127">이 항목의 [연결 만들기](connectors-create-api-onedrive.md#create-the-connection)에서 단계가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d73d7-128">이 예제에서는 선택한 폴더의 파일이 업데이트되면 논리 앱이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="d73d7-129">이 트리거의 결과를 보려면 전자 메일을 보내는 다른 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="d73d7-130">예를 들어 파일이 업데이트될 때 전자 메일을 보내는 Office 365 Outlook *전자 메일 보내기* 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="d73d7-131">**편집** 단추를 선택하고 **빈도** 및 **간격** 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="d73d7-132">예를 들어 15분마다 폴링을 트리거하려면 **빈도**를 **분**으로, **간격**을 **15**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="d73d7-133">변경 내용을 **저장**합니다(도구 모음 왼쪽 위 모서리).</span><span class="sxs-lookup"><span data-stu-id="d73d7-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="d73d7-134">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="d73d7-135">작업 사용</span><span class="sxs-lookup"><span data-stu-id="d73d7-135">Use an action</span></span>
<span data-ttu-id="d73d7-136">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="d73d7-137">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="d73d7-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="d73d7-138">더하기 기호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-138">Select the plus sign.</span></span> <span data-ttu-id="d73d7-139">**작업 추가**, **조건 추가** 또는 **자세히** 옵션 중 하나 등 몇 가지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="d73d7-140">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="d73d7-141">텍스트 상자에 "onedrive"를 입력하여 사용 가능한 모든 작업의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="d73d7-142">이 예제에서는 **OneDrive - 파일 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="d73d7-143">연결이 이미 존재하는 경우 **폴더 경로**를 선택하여 파일을 입력하고 **파일 이름**을 입력한 후 원하는 **파일 콘텐츠**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="d73d7-144">연결 정보를 묻는 메시지가 표시되면 연결을 만들기 위한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="d73d7-145">이 항목의 [연결 만들기](connectors-create-api-onedrive.md#create-the-connection)에서는 이러한 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d73d7-146">이 예제에서는 OneDrive 폴더에 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="d73d7-147">다른 트리거의 출력을 사용하여 OneDrive 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="d73d7-148">예를 들어 Office 365 Outlook *새 전자 메일이 도착했을 때* 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="d73d7-149">그런 후 ForEach 내에서 Attachments 및 Content-Type 필드를 사용하는 OneDrive *파일 만들기* 작업을 추가하여 OneDrive에서 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="d73d7-150">변경 내용을 **저장**합니다(도구 모음 왼쪽 위 모서리).</span><span class="sxs-lookup"><span data-stu-id="d73d7-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="d73d7-151">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="d73d7-152">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="d73d7-152">Connector-specific details</span></span>

<span data-ttu-id="d73d7-153">[커넥터 세부 정보](/connectors/onedriveconnector/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d73d7-154">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="d73d7-154">More connectors</span></span>
<span data-ttu-id="d73d7-155">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d73d7-155">Go back to the [APIs list](apis-list.md).</span></span>