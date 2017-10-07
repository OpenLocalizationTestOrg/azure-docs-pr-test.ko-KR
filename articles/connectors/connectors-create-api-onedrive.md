---
title: "논리 앱에서 aaaAdd hello OneDrive 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용 하는 hello OneDrive 커넥터 개요"
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
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="c3a1d-103">Hello OneDrive 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="c3a1d-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="c3a1d-104">TooOneDrive toomanage 업로드, get, 파일, 삭제 등을 포함 한 파일을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="c3a1d-105">OneDrive를 사용하여 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="c3a1d-106">OneDrive에서 파일을 저장하여 워크플로를 작성하거나 OneDrive의 기존 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="c3a1d-107">파일을 생성 하거나 OneDrive 내에서 업데이트 하는 경우 트리거 toostart 워크플로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="c3a1d-108">파일을 삭제를 작업 toocreate 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="c3a1d-109">예를 들어 새 Office 365 전자 메일이 첨부 파일과 함께 수신되면(트리거) OneDrive에 새 파일을 만듭니다(작업).</span><span class="sxs-lookup"><span data-stu-id="c3a1d-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="c3a1d-110">이 항목에서는 방법을 toouse hello 논리 앱에서 OneDrive 커넥터 및 트리거 및 작업 그룹의 hello도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="c3a1d-111">논리 앱에 대해 자세히 toolearn 참조 [논리 앱 이란](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="c3a1d-112">TooOneDrive 연결</span><span class="sxs-lookup"><span data-stu-id="c3a1d-112">Connect tooOneDrive</span></span>
<span data-ttu-id="c3a1d-113">논리 앱에서 모든 서비스에 액세스 하기 전에 먼저 만들어야는 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="c3a1d-114">연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="c3a1d-115">예를 들어, tooconnect tooOneDrive 먼저 OneDrive *연결*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="c3a1d-116">toocreate 연결을 일반적으로 tooconnect를 원하는 tooaccess hello 서비스를 사용 하는 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="c3a1d-117">따라서 OneDrive를 사용 hello tooyour OneDrive 계정 toocreate hello 연결 시 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="c3a1d-118">Hello 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="c3a1d-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="c3a1d-119">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="c3a1d-119">Use a trigger</span></span>
<span data-ttu-id="c3a1d-120">트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="c3a1d-121">트리거 "서비스를 폴링하기" hello 간격 및 원하는 빈도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="c3a1d-122">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="c3a1d-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="c3a1d-123">Hello 논리 앱에서 "onedrive" tooget hello 트리거 목록을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="c3a1d-124">**파일을 수정할 때**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-124">Select **When a file is modified**.</span></span> <span data-ttu-id="c3a1d-125">연결이 이미 존재 하는 경우에 hello 선택 표시 단추 tooselect 폴더를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="c3a1d-126">증명된 toosign 인 경우 hello 로그인 세부 정보 toocreate hello 연결에을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="c3a1d-127">[Hello 연결을 만들](connectors-create-api-onedrive.md#create-the-connection) 이 항목의 hello 단계를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c3a1d-128">이 예제에서는 hello 논리 앱 업데이트를 선택 하는 hello 폴더에 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="c3a1d-129">이 트리거의 toosee hello 결과 전자 메일을 보내는 다른 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="c3a1d-130">예를 들어 Office 365 Outlook hello 추가 *전자 메일 보내기* 파일 업데이트 될 때 전자 메일로 보내면 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="c3a1d-131">선택 hello **편집** 단추 및 hello 설정 **주파수** 및 **간격** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="c3a1d-132">예를 들어 15 분 마다 hello 트리거 toopoll 하려는 경우 다음 설정 hello **주파수** 너무**분**, 및 집합 hello **간격** 너무**15**.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="c3a1d-133">**저장** 변경 내용을 (hello 도구 모음의 왼쪽된 상단 모서리).</span><span class="sxs-lookup"><span data-stu-id="c3a1d-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="c3a1d-134">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="c3a1d-135">작업 사용</span><span class="sxs-lookup"><span data-stu-id="c3a1d-135">Use an action</span></span>
<span data-ttu-id="c3a1d-136">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="c3a1d-137">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="c3a1d-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="c3a1d-138">Hello 더하기 기호를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-138">Select hello plus sign.</span></span> <span data-ttu-id="c3a1d-139">여러 선택 항목을 참조 하십시오: **동작 추가**, **조건을 추가**, hello 중 하나 또는 **자세한** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="c3a1d-140">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="c3a1d-141">Hello 텍스트 상자에 "onedrive" tooget hello 사용 가능한 모든 작업 목록을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="c3a1d-142">이 예제에서는 **OneDrive - 파일 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="c3a1d-143">연결이 이미 존재 하는 경우 다음 hello 선택 **폴더 경로** tooput hello 파일, 입력 hello **파일 이름**, hello를 선택 하 고 **파일 콘텐츠** 원하는:</span><span class="sxs-lookup"><span data-stu-id="c3a1d-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="c3a1d-144">Hello 연결 정보에 대 한 메시지가 표시 되 면 hello, toocreate hello 연결 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="c3a1d-145">[Hello 연결을 만들](connectors-create-api-onedrive.md#create-the-connection) 이 항목에서 이러한 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c3a1d-146">이 예제에서는 OneDrive 폴더에 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="c3a1d-147">다른 트리거 toocreate hello OneDrive 파일에서 출력을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="c3a1d-148">예를 들어 Office 365 Outlook hello 추가 *새 전자 메일 도착* 트리거.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="c3a1d-149">다음 추가 hello OneDrive *파일 만들기* hello 첨부 파일 및 콘텐츠 형식 필드를 사용 하 여 OneDrive에 ForEach toocreate hello 새 파일 내에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="c3a1d-150">**저장** 변경 내용을 (hello 도구 모음의 왼쪽된 상단 모서리).</span><span class="sxs-lookup"><span data-stu-id="c3a1d-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="c3a1d-151">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="c3a1d-152">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="c3a1d-152">Connector-specific details</span></span>

<span data-ttu-id="c3a1d-153">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/onedriveconnector/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c3a1d-154">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="c3a1d-154">More connectors</span></span>
<span data-ttu-id="c3a1d-155">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3a1d-155">Go back toohello [APIs list](apis-list.md).</span></span>
