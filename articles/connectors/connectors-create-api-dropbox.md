---
title: "Azure Logic Apps의 Dropbox 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. Dropbox에 연결하여 파일을 관리합니다. Dropbox에서 파일 업로드, 업데이트, 가져오기 및 삭제와 같은 다양한 작업을 수행할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0d09580c60fd620811b539147439d0922839fe7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-dropbox-connector"></a><span data-ttu-id="9c5ed-105">Dropbox 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="9c5ed-105">Get started with the Dropbox connector</span></span>
<span data-ttu-id="9c5ed-106">Dropbox에 연결하여 파일을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-106">Connect to Dropbox to manage your files.</span></span> <span data-ttu-id="9c5ed-107">Dropbox에서 파일 업로드, 업데이트, 가져오기 및 삭제와 같은 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="9c5ed-108">[커넥터](apis-list.md)를 사용하려면 먼저 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="9c5ed-109">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-dropbox"></a><span data-ttu-id="9c5ed-110">Dropbox에 연결</span><span class="sxs-lookup"><span data-stu-id="9c5ed-110">Connect to Dropbox</span></span>
<span data-ttu-id="9c5ed-111">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="9c5ed-112">연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="9c5ed-113">예를 들어 Dropbox에 연결하려면 먼저 Dropbox *연결*이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="9c5ed-114">연결을 만들려면 연결하려는 서비스에 액세스할 때 일반적으로 사용하는 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="9c5ed-115">따라서 Dropbox 예제에서는 Dropbox에 대한 연결을 만들기 위해 Dropbox 계정에 대한 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span></span> [<span data-ttu-id="9c5ed-116">연결에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="9c5ed-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-to-dropbox"></a><span data-ttu-id="9c5ed-117">Dropbox에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="9c5ed-117">Create a connection to Dropbox</span></span>
> [!INCLUDE [Steps to create a connection to Dropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="9c5ed-118">Dropbox 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="9c5ed-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="9c5ed-119">트리거는 논리 앱에 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="9c5ed-120">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="9c5ed-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="9c5ed-121">이 예제에서는 **파일을 만들 때** 트리거를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-121">In this example, we will use the **When a file is created** trigger.</span></span> <span data-ttu-id="9c5ed-122">이 트리거가 발생하면 **경로를 사용하여 파일 콘텐츠 가져오기** Dropbox 작업을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="9c5ed-123">논리 앱 디자이너의 검색 상자에 *dropbox*를 입력한 후 **Dropbox - 파일을 만들 때** 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="9c5ed-124">파일 생성을 추적할 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-124">Select the folder in which you want to track file creation.</span></span> <span data-ttu-id="9c5ed-125">...(빨간색 상자에 표시)를 선택하고 트리거의 입력을 선택할 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="9c5ed-126">Dropbox 작업 사용</span><span class="sxs-lookup"><span data-stu-id="9c5ed-126">Use a Dropbox action</span></span>
<span data-ttu-id="9c5ed-127">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="9c5ed-128">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="9c5ed-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="9c5ed-129">이제 트리거가 추가되었고 다음 단계에 따라 새 파일의 콘텐츠를 가져올 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span></span>

1. <span data-ttu-id="9c5ed-130">**+ 새 단계**를 선택하여 새 파일을 만들 때 수행할 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="9c5ed-131">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-131">Select **Add an action**.</span></span> <span data-ttu-id="9c5ed-132">수행할 동작을 검색할 수 있는 검색 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="9c5ed-133">*dropbox*를 입력하여 Dropbox와 관련된 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-133">Enter *dropbox* to search for actions related to Dropbox.</span></span>  
4. <span data-ttu-id="9c5ed-134">선택한 Dropbox 폴더에서 새 파일이 생성될 때 수행할 작업으로 **Dropbox - 경로를 사용하여 파일 콘텐츠 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span></span> <span data-ttu-id="9c5ed-135">작업 제어 블록이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-135">The action control block opens.</span></span> <span data-ttu-id="9c5ed-136">논리 앱에 Dropbox 계정에 액세스하기 위한 권한을 아직 부여하지 않았으면 이러한 권한을 부여하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="9c5ed-137">...(**파일 경로** 컨트롤의 오른쪽에 있음)를 선택하고 사용할 파일 경로를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span></span> <span data-ttu-id="9c5ed-138">또는 **파일 경로** 토큰을 사용하여 빠르게 논리 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-138">Or, use the **file path** token to speed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="9c5ed-139">작업을 저장하고 Dropbox에 새 파일을 만들어 워크플로를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-139">Save your work and create a new file in Dropbox to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="9c5ed-140">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="9c5ed-140">Connector-specific details</span></span>

<span data-ttu-id="9c5ed-141">[커넥터 세부 정보](/connectors/dropbox/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-141">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="9c5ed-142">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="9c5ed-142">More connectors</span></span>
<span data-ttu-id="9c5ed-143">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="9c5ed-143">Go back to the [APIs list](apis-list.md).</span></span>