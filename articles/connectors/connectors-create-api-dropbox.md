---
title: "Azure 논리 앱에서 aaaDropbox 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. TooDropbox toomanage 파일을 연결 합니다. Dropbox에서 파일 업로드, 업데이트, 가져오기 및 삭제와 같은 다양한 작업을 수행할 수 있습니다."
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
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="07b9d-105">Hello Dropbox 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="07b9d-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="07b9d-106">TooDropbox toomanage 파일을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="07b9d-107">Dropbox에서 파일 업로드, 업데이트, 가져오기 및 삭제와 같은 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="07b9d-108">toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="07b9d-109">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="07b9d-110">TooDropbox 연결</span><span class="sxs-lookup"><span data-stu-id="07b9d-110">Connect tooDropbox</span></span>
<span data-ttu-id="07b9d-111">Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="07b9d-112">연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="07b9d-113">예를 들어 순서 tooconnect tooDropbox에서 먼저 Dropbox *연결*합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="07b9d-114">연결 toocreate tooprovide hello 자격 증명을 tooconnect 원하는 tooaccess hello 서비스를 일반적으로 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="07b9d-115">따라서 hello Dropbox 예에서 hello 자격 증명 tooyour 순서 toocreate hello 연결 tooDropbox에서 Dropbox 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> [<span data-ttu-id="07b9d-116">연결에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="07b9d-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="07b9d-117">연결 tooDropbox 만들기</span><span class="sxs-lookup"><span data-stu-id="07b9d-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="07b9d-118">Dropbox 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="07b9d-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="07b9d-119">트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="07b9d-120">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="07b9d-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="07b9d-121">이 예제에서는 hello 사용 **파일을 만들 때** 트리거.</span><span class="sxs-lookup"><span data-stu-id="07b9d-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="07b9d-122">이 트리거가 발생할 때이 라 hello **경로 사용 하는 파일 콘텐츠를 가져옵니다.** Dropbox 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="07b9d-123">입력 *dropbox* hello 논리 앱 디자이너에 hello 검색 상자에 다음 hello 선택 **Dropbox-파일을 만들 때** 트리거.</span><span class="sxs-lookup"><span data-stu-id="07b9d-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="07b9d-124">Tootrack 파일 만들기를 원하는 hello 폴더를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="07b9d-125">선택... (hello 빨간색 상자에서 식별 됨) 및 찾아보기 toohello 폴더 tooselect hello 트리거를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="07b9d-126">Dropbox 작업 사용</span><span class="sxs-lookup"><span data-stu-id="07b9d-126">Use a Dropbox action</span></span>
<span data-ttu-id="07b9d-127">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="07b9d-128">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="07b9d-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="07b9d-129">Hello 트리거 추가 했으므로 다음 단계 tooadd을 hello 새 파일의 콘텐츠를 받을 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="07b9d-130">선택 **+ 새 단계** tooadd hello 작업 원하는 tootake 새 파일을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="07b9d-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="07b9d-131">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-131">Select **Add an action**.</span></span> <span data-ttu-id="07b9d-132">검색할 수 있는 모든 작업에 대 한 있습니다이 열립니다 hello 검색 상자 tootake를 것인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="07b9d-133">입력 *dropbox* toosearch 관련된 tooDropbox 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="07b9d-134">선택 **Dropbox-파일 내용 가져오기 경로 사용 하 여** 동작 tootake hello hello 새 파일을 만들 때 선택 된 것으로 Dropbox 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="07b9d-135">hello 동작 제어 블록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-135">hello action control block opens.</span></span> <span data-ttu-id="07b9d-136">하면 하지 않았으면 지금 이전에 Dropbox 계정을 하 여 논리 앱 tooaccess tooauthorize 메시지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="07b9d-137">선택... (hello의 hello 오른쪽에 있는 **파일 경로** 컨트롤) toouse 원하는 toohello 파일 경로 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="07b9d-138">Hello를 사용 하 여 또는 **파일 경로** 토큰 toospeed 논리가 응용 프로그램 생성을 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="07b9d-139">작업 내용을 저장 하 고 Dropbox tooactivate 워크플로에 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="07b9d-140">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="07b9d-140">Connector-specific details</span></span>

<span data-ttu-id="07b9d-141">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/dropbox/)합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="07b9d-142">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="07b9d-142">More connectors</span></span>
<span data-ttu-id="07b9d-143">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07b9d-143">Go back toohello [APIs list](apis-list.md).</span></span>
