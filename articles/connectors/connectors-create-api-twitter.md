---
title: "aaaLearn 어떻게 toouse hello 논리 앱에서 Twitter 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 Twitter 커넥터 개요"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="a5622-103">Hello Twitter 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="a5622-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="a5622-104">Hello Twitter 커넥터와 함께 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="a5622-105">트윗 게시 및 트윗 가져오기</span><span class="sxs-lookup"><span data-stu-id="a5622-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="a5622-106">타임라인, 친구 및 팔로워 액세스</span><span class="sxs-lookup"><span data-stu-id="a5622-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="a5622-107">다른 동작 및 트리거 아래에 설명 된 hello를 수행</span><span class="sxs-lookup"><span data-stu-id="a5622-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="a5622-108">toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="a5622-109">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="a5622-110">TooTwitter 연결</span><span class="sxs-lookup"><span data-stu-id="a5622-110">Connect tooTwitter</span></span>
<span data-ttu-id="a5622-111">Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="a5622-112">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="a5622-113">연결 tooTwitter 만들기</span><span class="sxs-lookup"><span data-stu-id="a5622-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="a5622-114">Twitter 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="a5622-114">Use a Twitter trigger</span></span>
<span data-ttu-id="a5622-115">트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="a5622-116">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="a5622-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="a5622-117">이 예제에서는 하겠습니다 어떻게 toouse hello **새 윗이 게시 될 때** #Seattle에 대 한 toosearch 트리거되며 #Seattle 있더라도 hello 텍스트 hello 윗을 Dropbox에 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="a5622-118">엔터프라이즈 예제에서는 회사의 hello 이름에 대 한 검색 하 고 hello 텍스트 hello 윗에서 SQL 데이터베이스 업데이트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="a5622-119">입력 *twitter* hello 논리 앱 디자이너에 hello 검색 상자에 다음 hello 선택 **Twitter-새 윗 게시 될 때** 트리거</span><span class="sxs-lookup"><span data-stu-id="a5622-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="a5622-120">![Twitter 트리거 이미지 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="a5622-121">입력 *#Seattle* hello에 **검색 텍스트** 컨트롤</span><span class="sxs-lookup"><span data-stu-id="a5622-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="a5622-122">![Twitter 트리거 이미지 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="a5622-123">이 시점에서 다른 트리거 및 작업 hello 워크플로에서 hello에 대 한 실행을 시작 합니다 트리거 논리 앱 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="a5622-124">기능 논리 앱 toobe는, 하나 이상의 트리거와 작업을 하나 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="a5622-125">Hello 다음 섹션 tooadd 동작의에서 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="a5622-126">조건 추가</span><span class="sxs-lookup"><span data-stu-id="a5622-126">Add a condition</span></span>
<span data-ttu-id="a5622-127">50 개 이상의 사용자와 사용자 로부터 트 윗에만 관심이, 이후 후속 작업이 hello 수를 확인 하는 조건은 먼저 추가 해야 toohello 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="a5622-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="a5622-128">선택 **+ 새 단계** tooadd hello 작업 원하는 tootake #Seattle 새 윗에서 발견 된 경우</span><span class="sxs-lookup"><span data-stu-id="a5622-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="a5622-129">![Twitter 작업 이미지 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="a5622-130">선택 hello **조건 추가** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="a5622-131">![Twitter 조건 이미지 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="a5622-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="a5622-132">Hello 열립니다 **조건** 제어와 같은 상태를 확인할 수는 위치 *같으면*, *는 보다 작은*, *보다 크면*, *포함*등입니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="a5622-133">![Twitter 조건 이미지 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="a5622-134">선택 hello **값 선택** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="a5622-135">이 컨트롤의 조건을 평가 tootrue 또는 false가 됩니다 hello 값으로 hello 속성 중 하나 이상을 트리거 하거나 모든 이전 작업에서에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="a5622-136">![Twitter 조건 이미지 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="a5622-137">선택 hello **...**  tooexpand hello 목록이 속성 사용할 수 있는 모든 hello 속성을 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="a5622-138">![Twitter 조건 이미지 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="a5622-139">선택 hello **후속 작업이 count** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="a5622-140">![Twitter 조건 이미지 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="a5622-141">공지 hello 후속 작업이 count 속성 hello 값 컨트롤에 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Twitter 조건 이미지 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="a5622-143">선택 **보다 크면** hello 연산자 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="a5622-144">![Twitter 조건 이미지 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="a5622-145">Hello에 대 한 피연산자 hello 50 입력 *보다 크면* 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="a5622-146">hello 조건이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-146">hello condition is now added.</span></span> <span data-ttu-id="a5622-147">Hello를 사용 하 여 작업을 저장 **저장** 위의 hello 메뉴에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="a5622-148">![Twitter 조건 이미지 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="a5622-149">Twitter 작업 사용</span><span class="sxs-lookup"><span data-stu-id="a5622-149">Use a Twitter action</span></span>
<span data-ttu-id="a5622-150">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="a5622-151">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="a5622-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="a5622-152">트리거를 추가 하면 했으므로 다음 단계 tooadd hello 트리거가 여 hello 트 윗의 hello 내용으로 새 윗에서 게시 하는 동작을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="a5622-153">이 연습의 목적 hello에 대 한가 50 개 이상의 후속 작업이 있는 사용자의 윗만 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="a5622-154">Hello 다음 단계에서 50 개 이상의 후속 작업이 가진 사용자가 게시 된 각 윗의 hello 속성 중 일부를 사용 하 여 트 윗 게시할 Twitter 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="a5622-155">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-155">Select **Add an action**.</span></span> <span data-ttu-id="a5622-156">이렇게 하면 다른 동작 및 트리거를 검색할 수 있는 hello 검색 컨트롤을 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="a5622-157">![Twitter 조건 이미지 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="a5622-158">입력 *twitter* hello 검색 상자에 다음 hello 선택 **Twitter-여 트 윗 게시** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="a5622-159">Hello 열립니다 **여 트 윗 게시** 입력할 수 있는 모든 세부 사항을 게시 되는 hello 트 윗에 대 한 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="a5622-160">![Twitter 작업 이미지 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="a5622-161">선택 hello **텍스트 윗** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="a5622-162">이전 동작 및 트리거 hello 논리 앱에서의 모든 출력에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="a5622-163">이러한 항목 중 하나를 선택할 수 있으며 hello 새 윗의 hello 윗 텍스트의 일부로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="a5622-164">![Twitter 작업 이미지 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="a5622-165">**사용자 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-165">Select **User name**</span></span>   
5. <span data-ttu-id="a5622-166">입력 *표시:* hello 윗 텍스트 컨트롤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="a5622-167">사용자 이름 바로 뒤에 나오도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="a5622-168">*트윗 텍스트*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="a5622-169">![Twitter 작업 이미지 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="a5622-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="a5622-170">작업 내용을 저장 하 고 워크플로 hello #Seattle hashtag tooactivate와 한 트 윗을 보낼 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="a5622-171">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="a5622-171">Connector-specific details</span></span>

<span data-ttu-id="a5622-172">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/twitterconnector/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5622-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a5622-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5622-173">Next steps</span></span>
[<span data-ttu-id="a5622-174">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a5622-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

