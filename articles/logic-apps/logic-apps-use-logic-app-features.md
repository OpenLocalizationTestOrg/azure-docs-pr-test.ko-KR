---
title: "aaaAdd 조건과 워크플로-Azure 논리 앱 시작 | Microsoft Docs"
description: "조건부 논리, 트리거, 동작 및 매개 변수를 추가하여 Azure Logic Apps에서 워크플로가 실행되는 방식을 제어합니다."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="50c24-103">논리 앱 기능 사용</span><span class="sxs-lookup"><span data-stu-id="50c24-103">Use Logic Apps features</span></span>

<span data-ttu-id="50c24-104">[이전 항목](../logic-apps/logic-apps-create-a-logic-app.md)에서는 첫 번째 논리 앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="50c24-105">toocontrol 논리 앱의 워크플로 논리 앱 toorun에 대 한 서로 다른 경로 지정 하 고 어떻게 너무 배열, 컬렉션 및 일괄 처리에서 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="50c24-106">논리 앱 워크플로에 포함될 수 있는 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="50c24-107">조건 및 [switch 문](../logic-apps/logic-apps-switch-case.md) - 특정 조건이 충족되는지 여부에 따라 논리 앱에서 다른 동작을 실행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="50c24-108">[루프](../logic-apps/logic-apps-loops-and-scopes.md) - 논리 앱에서 단계를 반복적으로 실행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="50c24-109">예를 들어 **For_each** 루프를 사용할 때 배열에 대해 동작을 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="50c24-110">또는 **Until** 루프를 사용할 때 조건이 충족될 때까지 동작을 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="50c24-111">[범위](../logic-apps/logic-apps-loops-and-scopes.md) 함께 그룹화 할 일련의 동작, 예를 들어 let tooimplement 예외 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="50c24-112">[인증](../logic-apps/logic-apps-loops-and-scopes.md) hello를 사용 하는 경우 배열의 항목에 대 한 별도 워크플로 시작 하 여 논리 앱을 사용 하면 있습니다 **SplitOn** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="50c24-113">이 항목에서는 논리 앱을 빌드하기 위한 다른 개념에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="50c24-114">보기 tooedit 기존 논리 앱 코드</span><span class="sxs-lookup"><span data-stu-id="50c24-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="50c24-115">워크플로 시작 옵션</span><span class="sxs-lookup"><span data-stu-id="50c24-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="50c24-116">조건: 조건 충족 후에만 단계 실행</span><span class="sxs-lookup"><span data-stu-id="50c24-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="50c24-117">toohave 데이터 특정 조건을 충족 하는 경우에 단계를 실행 하 여 논리 앱을 특정 필드 또는 값에 대 한 hello 워크플로에서 데이터를 비교 하는 조건을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="50c24-118">예를 들어 웹 사이트의 RSS 피드에 있는 게시물에 대해 너무 많은 전자 메일을 보내는 논리 앱이 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="50c24-119">조건이 논리 앱 hello 새 게시 하는 경우에 전자 메일을 보내 있도록 속한 tooa 특정 범주를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="50c24-120">Hello에 [Azure 포털](https://portal.azure.com), 찾기 및 논리 앱 논리 응용 프로그램 디자이너에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="50c24-121">원하는 조건을 toohello 워크플로 위치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="50c24-122">기존 hello 논리 앱 워크플로 단계 사이 tooadd hello 조건을 hello 포인터 위로 이동 hello 화살표 저장할 tooadd hello 조건.</span><span class="sxs-lookup"><span data-stu-id="50c24-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="50c24-123">Hello 선택 **더하기 기호** (**+**)를 선택 합니다 **조건 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="50c24-124">예:</span><span class="sxs-lookup"><span data-stu-id="50c24-124">For example:</span></span>

   ![조건 toologic 앱 추가](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="50c24-126">현재 워크플로의 hello 끝 조건을 tooadd를 원하는 경우 논리 앱의 toohello 아래쪽 이동 고 **+ 새 단계**합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="50c24-127">이제 hello 조건을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-127">Now define hello condition.</span></span> <span data-ttu-id="50c24-128">Tooevaluate, hello 작업 tooperform 및 hello 대상 값 또는 필드 원하는 hello 소스 필드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="50c24-129">tooyour 조건 필드 tooadd 기존 hello 중에서 선택할 **동적 콘텐츠 목록에 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="50c24-130">예:</span><span class="sxs-lookup"><span data-stu-id="50c24-130">For example:</span></span>

   ![기본 모드에서 조건 편집](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="50c24-132">Hello 완전 한 조건이 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-132">Here's hello complete condition:</span></span>

   ![완성된 조건](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="50c24-134">코드에서 toodefine hello 조건 선택 **고급 모드에서 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="50c24-135">예:</span><span class="sxs-lookup"><span data-stu-id="50c24-135">For example:</span></span>
   > 
   > ![코드에서 조건 편집](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="50c24-137">아래 **IF 예** 및 **IF 아니요**, hello 단계 tooperform hello 조건 충족 여부에 따라 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="50c24-138">예:</span><span class="sxs-lookup"><span data-stu-id="50c24-138">For example:</span></span>

   ![YES 및 NO 경로가 있는 조건](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="50c24-140">Hello에 기존 작업을 끌어올 수 **IF 예** 및 **IF 아니요** 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="50c24-141">완료되면 논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="50c24-142">이제 hello 게시물에 조건을 충족 하는 경우에 전자 메일 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="50c24-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="50c24-143">forEach를 포함한 목록에 작업 반복</span><span class="sxs-lookup"><span data-stu-id="50c24-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="50c24-144">forEach 루프 hello 위에 배열 toorepeat 동작을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="50c24-145">배열이 없는 경우 hello 흐름 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="50c24-146">예를 들어 메시지의 배열을 출력 action1 있고 toosend 각 메시지를 원하는 경우 액션의 hello 속성에서이 forEach 문을 포함할 수 있습니다.`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="50c24-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="50c24-147">논리 앱에 대 한 hello 코드 정의 편집</span><span class="sxs-lookup"><span data-stu-id="50c24-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="50c24-148">Hello 논리가 응용 프로그램 디자이너를 사용 하는 있지만 논리 앱 정의 하는 hello 코드를 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="50c24-149">Hello 명령 모음에서 **코드 뷰**합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="50c24-150">전체 편집기가 열리고 편집한 hello 정의 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-150">A full editor opens and shows hello definition you edited.</span></span>

    ![코드 보기](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="50c24-152">Hello 텍스트 편집기에서 복사 및 붙여넣기 수의 hello 내에서 작업 수 있습니다 같은 논리 앱 또는 논리 앱 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="50c24-153">또한 추가 하거나 hello 정의에서 전체 섹션을 제거할 수 있으며 정의 다른 사용자와 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="50c24-154">toosave 편집 내용을 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="50c24-155">매개 변수</span><span class="sxs-lookup"><span data-stu-id="50c24-155">Parameters</span></span>

<span data-ttu-id="50c24-156">일부 Logic Apps 기능은 매개 변수와 같은 코드 보기에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="50c24-157">매개 변수 논리 앱 전반에서 쉽게 tooreuse 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="50c24-158">예를 들어 여러 작업에서 사용할 메일 주소가 있는 경우 해당 전자 메일 주소를 매개 변수로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="50c24-159">매개 변수는 가능성이 toochange을 너무 많이 있는지 값을 추출 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="50c24-160">다양 한 환경에서 toooverride 매개 변수를 할 때 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="50c24-161">환경에 따라 toooverride 매개 변수를 확인 하려면 어떻게 toolearn [논리 앱 정의 작성](../logic-apps/logic-apps-author-definitions.md) 및 [REST API 문서](https://docs.microsoft.com/rest/api/logic)합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="50c24-162">이 예에서는 어떻게 tooupdate 기존 논리 앱 hello 쿼리 용어에 대 한 매개 변수를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="50c24-163">코드 뷰에서 찾을 hello `parameters : {}` 개체를 추가할는 `currentFeedUrl` 개체:</span><span class="sxs-lookup"><span data-stu-id="50c24-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="50c24-164">Toohello 이동 `When_a_feed-item_is_published` 작업, 찾기 hello `queries` 섹션 및 hello 쿼리 값을 바꿉니다.`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="50c24-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="50c24-165">toojoin 둘 이상의 문자열 hello를 사용할 수도 있습니다 `concat` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="50c24-166">예를 들어 `"@concat('#',parameters('currentFeedUrl'))"` works hello 위의 hello와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="50c24-167">완료하면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="50c24-168">Hello 웹 사이트의 RSS hello 통해 다른 URL을 전달 하 여 피드를 변경할 수 이제 `currentFeedURL` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="50c24-169">에 대 한 자세한 내용은 [어떻게 tooauthor 논리 앱 정의](../logic-apps/logic-apps-author-definitions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="50c24-170">논리 앱 워크플로 시작</span><span class="sxs-lookup"><span data-stu-id="50c24-170">Start logic app workflows</span></span>

<span data-ttu-id="50c24-171">논리 앱에 정의 된 hello 워크플로 시작 하기 위한 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="50c24-172">항상 hello에 대 한 요청 시 워크플로 시작 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="50c24-173">되풀이 트리거</span><span class="sxs-lookup"><span data-stu-id="50c24-173">Recurrence triggers</span></span>

<span data-ttu-id="50c24-174">되풀이 트리거는 지정한 간격마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="50c24-175">Hello 트리거에 조건부 논리, hello 트리거 hello 워크플로 toorun 필요한 지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="50c24-176">트리거를 반환 하 여 hello 워크플로가 실행 되는 나타냅니다는 `200` 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="50c24-177">Hello 워크플로 toorun 필요 하지 않습니다, hello 트리거 반환는 `202` 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="50c24-178">REST API를 사용한 콜백</span><span class="sxs-lookup"><span data-stu-id="50c24-178">Callback using REST APIs</span></span>

<span data-ttu-id="50c24-179">워크플로 toostart 서비스 논리 앱 끝점을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="50c24-180">이러한 종류의 논리가 응용 프로그램 요청 선택 toostart **지금 실행** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="50c24-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="50c24-181">[논리 앱 끝점을 트리거로 호출하여 워크플로 시작](../logic-apps/logic-apps-http-endpoint.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50c24-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[Azure 포털]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="50c24-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50c24-183">Next steps</span></span>

* [<span data-ttu-id="50c24-184">Switch 문</span><span class="sxs-lookup"><span data-stu-id="50c24-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="50c24-185">루프, 범위 및 분할</span><span class="sxs-lookup"><span data-stu-id="50c24-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="50c24-186">작성자 논리 앱 정의</span><span class="sxs-lookup"><span data-stu-id="50c24-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)