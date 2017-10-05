---
title: "논리 앱에서 Twitter 커넥터를 사용하는 방법 알아보기 | Microsoft Docs"
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
ms.openlocfilehash: be8163043535833ce45b3d50939a537406cf8152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twitter-connector"></a><span data-ttu-id="39a7b-103">Twitter 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="39a7b-103">Get started with the Twitter connector</span></span>
<span data-ttu-id="39a7b-104">Twitter 커넥터를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-104">With the Twitter connector you can:</span></span>

* <span data-ttu-id="39a7b-105">트윗 게시 및 트윗 가져오기</span><span class="sxs-lookup"><span data-stu-id="39a7b-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="39a7b-106">타임라인, 친구 및 팔로워 액세스</span><span class="sxs-lookup"><span data-stu-id="39a7b-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="39a7b-107">아래 설명된 기타 작업 및 트리거 수행</span><span class="sxs-lookup"><span data-stu-id="39a7b-107">Perform any of the other actions and triggers described below</span></span>  

<span data-ttu-id="39a7b-108">[커넥터](apis-list.md)를 사용하려면 먼저 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="39a7b-109">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-to-twitter"></a><span data-ttu-id="39a7b-110">Twitter에 연결</span><span class="sxs-lookup"><span data-stu-id="39a7b-110">Connect to Twitter</span></span>
<span data-ttu-id="39a7b-111">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="39a7b-112">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-twitter"></a><span data-ttu-id="39a7b-113">Twitter에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="39a7b-113">Create a connection to Twitter</span></span>
> [!INCLUDE [Steps to create a connection to Twitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="39a7b-114">Twitter 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="39a7b-114">Use a Twitter trigger</span></span>
<span data-ttu-id="39a7b-115">트리거는 논리 앱에 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="39a7b-116">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="39a7b-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="39a7b-117">이 예에서는 #Seattle을 검색하는 데 **새 트윗이 게시될 때** 트리거를 사용하고 #Seattle이 있는 경우 트윗의 텍스트로 Dropbox의 파일을 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-117">In this example, I will show you how to use the **When a new tweet is posted**  trigger to search for #Seattle and, if #Seattle is found, update a file in Dropbox with the text from the tweet.</span></span> <span data-ttu-id="39a7b-118">엔터프라이즈 예에서는 회사 이름을 검색하고 SQL 데이터베이스를 트윗의 텍스트로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-118">In an enterprise example, you could search for the name of your company and update a SQL database with the text from the tweet.</span></span>

1. <span data-ttu-id="39a7b-119">논리 앱 디자이너의 검색 상자에 *twitter*를 입력한 후 **Twitter - 새 트윗이 게시될 때** 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-119">Enter *twitter* in the search box on the logic apps designer then select the **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="39a7b-120">![Twitter 트리거 이미지 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="39a7b-121">**검색 텍스트** 컨트롤에 *#Seattle*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-121">Enter *#Seattle* in the **Search Text** control</span></span>  
   <span data-ttu-id="39a7b-122">![Twitter 트리거 이미지 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="39a7b-123">이제, 논리 앱은 워크플로의 다른 트리거 및 동작의 실행을 시작하는 트리거로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-123">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="39a7b-124">논리 앱이 작동하려면 하나 이상의 트리거와 작업이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-124">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="39a7b-125">다음 섹션의 단계에 따라 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-125">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="39a7b-126">조건 추가</span><span class="sxs-lookup"><span data-stu-id="39a7b-126">Add a condition</span></span>
<span data-ttu-id="39a7b-127">50명 이상의 사용자가 있는 사용자의 트윗에만 관심이 있는 경우 먼저 팔로워 수를 확인하는 조건을 논리 앱에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms the number of followers must first be added to the logic app.</span></span>  

1. <span data-ttu-id="39a7b-128">**+ 새 단계**를 선택하여 새 트윗에 #Seattle이 있을 때 수행할 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-128">Select **+ New step** to add the action you would like to take when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="39a7b-129">![Twitter 작업 이미지 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="39a7b-130">**조건 추가** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-130">Select the **Add a condition** link.</span></span>  
   <span data-ttu-id="39a7b-131">![Twitter 조건 이미지 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="39a7b-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="39a7b-132">그러면 *같음*, *보다 작음*, *보다 큼*, *포함* 등과 같은 조건을 확인할 수 있는 **조건** 컨트롤이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-132">This opens the **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="39a7b-133">![Twitter 조건 이미지 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="39a7b-134">**값 선택** 컨트롤을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-134">Select the **Choose a value** control.</span></span>  
   <span data-ttu-id="39a7b-135">이 컨트롤에서는 조건이 true 또는 false로 평가될 값으로 이전 작업 또는 트리거 중 하나 이상의 속성을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-135">In this control, you can select one or more of the properties from any previous actions or triggers as the value whose condition will be evaluated to true or false.</span></span>
   <span data-ttu-id="39a7b-136">![Twitter 조건 이미지 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="39a7b-137">**...**를 선택하여 속성 목록을 확장하면 사용 가능한 모든 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-137">Select the **...** to expand the list of properties so you can see all the properties that are available.</span></span>        
   <span data-ttu-id="39a7b-138">![Twitter 조건 이미지 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="39a7b-139">**팔로워 수** 속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-139">Select the **Followers count** property.</span></span>    
   <span data-ttu-id="39a7b-140">![Twitter 조건 이미지 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="39a7b-141">이제 팔로워 수 속성이 값 컨트롤에 있는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-141">Notice the Followers count property is now in the value control.</span></span>    
   ![Twitter 조건 이미지 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="39a7b-143">연산자 목록에서 **보다 큼**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-143">Select **is greater than** from the operators list.</span></span>    
   <span data-ttu-id="39a7b-144">![Twitter 조건 이미지 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="39a7b-145">*보다 큼* 연산자의 피연산자로 50을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-145">Enter 50 as the operand for the *is greater than* operator.</span></span>  
   <span data-ttu-id="39a7b-146">이제 조건이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-146">The condition is now added.</span></span> <span data-ttu-id="39a7b-147">위의 메뉴에서 **저장** 링크를 사용하여 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-147">Save your work using the **Save** link on the menu above.</span></span>    
   <span data-ttu-id="39a7b-148">![Twitter 조건 이미지 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="39a7b-149">Twitter 작업 사용</span><span class="sxs-lookup"><span data-stu-id="39a7b-149">Use a Twitter action</span></span>
<span data-ttu-id="39a7b-150">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-150">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="39a7b-151">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="39a7b-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="39a7b-152">이제 트리거를 추가했으므로 다음 단계에 따라 트리거가 찾은 트윗의 내용으로 새 트윗을 게시할 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-152">Now that you have added a trigger, follow these steps to add an action that will post a new tweet with the contents of the tweets found by the trigger.</span></span> <span data-ttu-id="39a7b-153">이 연습의 목적은 50명 이상의 팔로워가 있는 사용자의 트윗만 게시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-153">For the purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="39a7b-154">다음 단계에서는 50명 이상의 팔로워가 있는 사용자가 게시한 각 트윗의 일부 속성을 사용하여 트윗을 게시하는 Twitter 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-154">In the next step, you will add a Twitter action that will post a tweet using some of the properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="39a7b-155">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-155">Select **Add an action**.</span></span> <span data-ttu-id="39a7b-156">그러면 다른 작업 및 트리거를 검색할 수 있는 검색 컨트롤이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-156">This opens the search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="39a7b-157">![Twitter 조건 이미지 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="39a7b-158">검색 상자에 *twitter*를 입력한 후 **Twitter - 트윗 게시** 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-158">Enter *twitter* into the search box then select the **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="39a7b-159">그러면 트윗에 대해 게시되는 모든 세부 사항을 입력할 **트윗 게시** 컨트롤이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-159">This opens the **Post a tweet** control where you will enter all details for the tweet being posted.</span></span>      
   <span data-ttu-id="39a7b-160">![Twitter 작업 이미지 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="39a7b-161">**트윗 텍스트** 컨트롤을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-161">Select the **Tweet text** control.</span></span> <span data-ttu-id="39a7b-162">이제 논리 앱에서 이전 작업 및 트리거의 모든 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-162">All outputs from previous actions and triggers in the logic app are now visible.</span></span> <span data-ttu-id="39a7b-163">이러한 항목 중 어떤 것이나 선택하여 새 트윗의 일부 트윗 텍스트로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-163">You can select any of these and use them as part of the tweet text of the new tweet.</span></span>     
   <span data-ttu-id="39a7b-164">![Twitter 작업 이미지 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="39a7b-165">**사용자 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-165">Select **User name**</span></span>   
5. <span data-ttu-id="39a7b-166">트윗 텍스트 컨트롤에 *says:(님의 말:)*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-166">Enter *says:* in the tweet text control.</span></span> <span data-ttu-id="39a7b-167">사용자 이름 바로 뒤에 나오도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="39a7b-168">*트윗 텍스트*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="39a7b-169">![Twitter 작업 이미지 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="39a7b-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="39a7b-170">작업 내용을 저장하고 #Seattle 해시 태그로 트윗을 보내 워크플로를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-170">Save your work and send a tweet with the #Seattle hashtag to activate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="39a7b-171">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="39a7b-171">Connector-specific details</span></span>

<span data-ttu-id="39a7b-172">[커넥터 세부 정보](/connectors/twitterconnector/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39a7b-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="39a7b-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39a7b-173">Next steps</span></span>
[<span data-ttu-id="39a7b-174">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="39a7b-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

