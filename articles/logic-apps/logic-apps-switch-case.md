---
title: "Azure 논리 앱에서 다른 작업에 대해 aaaSwitch 문을 | Microsoft Docs"
description: "Switch 문을 사용 하 여 식 값에 따라 논리 앱의 동작이 서로 다른 tooperform 선택"
services: logic-apps
keywords: "Switch 문"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="46fa5-104">Switch 문으로 Logic Apps에서 다양한 작업 수행</span><span class="sxs-lookup"><span data-stu-id="46fa5-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="46fa5-105">워크플로 제작할 때 개체 또는 식의 hello 값에 따라 tootake 서로 다른 작업 종종 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="46fa5-106">예를 들어 hello 상태 코드는 HTTP 요청에 따라 다르게 하 여 논리 앱 toobehave 또는 전자 메일에서 선택한 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="46fa5-107">Switch 문 tooimplement 이러한 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="46fa5-108">논리 앱에서 식이나 토큰을 계산 하 고 hello로 hello 사례 선택 수 값 tooexecute hello 동일한 작업을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="46fa5-109">하나의 사례 hello switch 문의 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="46fa5-110">모든 프로그래밍 언어와 마찬가지로 Switch 문도 같음 연산자만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="46fa5-111">다른 관계형 연산자(예: “초과”)가 필요한 경우 조건문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="46fa5-112">tooensure 결정적 실행 동작의 경우 동적 토큰 또는 식 대신 고유 하 고 정적 값을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46fa5-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="46fa5-113">Prerequisites</span></span>

- <span data-ttu-id="46fa5-114">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="46fa5-114">An active Azure subscription.</span></span> <span data-ttu-id="46fa5-115">활성 Azure 구독이 없는 경우 시작하기 전에 [무료 계정을 만들거나](https://azure.microsoft.com/free/) [무료로 Logic Apps](https://tryappservice.azure.com/)을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="46fa5-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="46fa5-116">Logic Apps에 대한 기본 지식</span><span class="sxs-lookup"><span data-stu-id="46fa5-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="46fa5-117">Switch 문 tooyour 워크플로 추가</span><span class="sxs-lookup"><span data-stu-id="46fa5-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="46fa5-118">switch 문의 작동 원리 tooshow,이 예제 모니터 파일 업로드 tooDropbox 되었는지 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="46fa5-119">Hello 논리 앱 전자 메일 tooan 승인자에 게 보내는 hello 새 파일을 업로드 하는 경우 여부 tootransfer 파일 tooSharePoint 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="46fa5-120">hello 앱 승인자가 선택 되어 hello는 hello 값에 따라 다른 작업을 수행 하는 switch 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="46fa5-121">논리 앱을 만들고 **Dropbox - 파일을 만들 경우** 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Dropbox - 파일을 만들 경우 트리거 사용](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="46fa5-123">Hello 트리거 아래에서이 작업을 추가: **Outlook.com-전자 메일을 보내기 승인**</span><span class="sxs-lookup"><span data-stu-id="46fa5-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="46fa5-124">또한 Logic Apps는 Office 365 Outlook 계정에서 승인 전자 메일을 보내는 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="46fa5-125">기존 연결 되지 않은 경우 메시지가 toocreate 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="46fa5-126">Hello 필수 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-126">Fill in hello required fields.</span></span> <span data-ttu-id="46fa5-127">예를 들어 아래 **를**, hello 승인자 전자 메일을 보내기 위한 hello 전자 메일 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="46fa5-128">**사용자 옵션**에서 `Approve, Reject`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![연결 구성](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="46fa5-130">Switch 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-130">Add a switch statement.</span></span>

   - <span data-ttu-id="46fa5-131">**+ 새 단계** > **... 추가 정보** > **Switch 사례 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="46fa5-132">이제 tooselect hello 동작 tooperform hello에 따라 원하는 `SelectedOptions` hello에서 출력 *승인 전자 메일을 보낼* 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="46fa5-133">Hello에서이 필드를 찾을 수 있습니다 **동적 콘텐츠를 추가할** 선택기입니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="46fa5-134">사용 하 여 *사례 1* hello 승인자를 선택 했을 때 toohandle `Approve`합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="46fa5-135">승인 되 면 hello 원래 파일 tooSharePoint 온라인 hello로 복사 [ **SharePoint Online-파일을 만들** 동작](../connectors/connectors-create-api-sharepointonline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="46fa5-136">새 파일을 SharePoint에서 사용할 수 있는 hello 사례 toonotify 사용자에서 다른 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="46fa5-137">사용자가을 선택할 때 다른 사례 toohandle 추가 `Reject`합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="46fa5-138">거부 되 면 hello 파일 거부 되 고 추가 조치가 필요 하지 않습니다 다른 승인자에 게 알리는 알림 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="46fa5-139">`SelectedOptions`hello 삭제할 수 있습니다. 되므로 두 개의 옵션을 제공 **기본** 경우 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Switch 문](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="46fa5-141">Switch 문 또한 toohello 기본적인 경우 대/소문자를 하나 이상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="46fa5-142">Hello switch 문의 한 후이 작업을 추가 하 여 hello 원래 업로드 한 파일 tooDropbox 삭제할: **Dropbox-파일 삭제**</span><span class="sxs-lookup"><span data-stu-id="46fa5-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="46fa5-143">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-143">Save your logic app.</span></span> <span data-ttu-id="46fa5-144">파일 tooDropbox 업로드 하 여 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="46fa5-145">곧 승인 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="46fa5-146">옵션을 선택 하 고 hello 동작을 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="46fa5-147">방법에 대해 너무 확인[논리 앱 모니터링](logic-apps-monitor-your-logic-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="46fa5-148">Switch 문 뒤에 있는 hello 코드 이해</span><span class="sxs-lookup"><span data-stu-id="46fa5-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="46fa5-149">Switch 문을 사용 하 여 논리 앱을 성공적으로 만든 hello switch 문의 뒤 hello 코드 정의에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="46fa5-150">`"Switch"`hello hello switch 문의 가독성을 높이기 위해 이름을 바꿀 수 있는 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="46fa5-151">`"type": "Switch"`hello 동작은 switch 문을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="46fa5-152">`"expression"`이 예에서 hello 승인자 선택한 옵션이 며 hello 정의 나중에 선언 된 각 사례에 대해 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="46fa5-153">`"cases"`은 임의의 사례 수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="46fa5-154">각 사례에 대해 `"Case *"` hello hello 소문자 가독성을 높이기 위해 이름을 바꿀 수 있습니다를 기본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="46fa5-155">`"case"`비교를 위해 사용 되는 스위치 식 hello 지속적이 고 고유한 값 이어야 하며 hello case 레이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="46fa5-156">Hello switch 식에서 작업 하는 경우 필드 hello 사례 중 일치 하는 `"default"` 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="46fa5-157">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="46fa5-157">Get help</span></span>

<span data-ttu-id="46fa5-158">tooask 질문과 대답 질문 참조를 수행 하는 다른 Azure 논리 앱 사용자가 방문 hello [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="46fa5-159">Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [Azure 논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46fa5-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46fa5-160">Next steps</span></span>

- <span data-ttu-id="46fa5-161">너무 방법에 대해 알아봅니다[조건 추가](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="46fa5-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="46fa5-162">[오류 및 예외 처리](logic-apps-exception-handling.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="46fa5-163">[워크플로 언어 기능](logic-apps-author-definitions.md)을 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="46fa5-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>