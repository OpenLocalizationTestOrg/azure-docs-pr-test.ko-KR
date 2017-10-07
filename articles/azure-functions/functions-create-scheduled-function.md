---
title: "Azure에서 일정에 따라 실행 하는 함수 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate는 함수를 실행 하는 Azure의 기반으로 사용자가 정의한 일정에 알아봅니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="0df3d-103">Azure에서 타이머에 따라 트리거되는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="0df3d-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="0df3d-104">어떻게 toouse Azure 함수 toocreate를 실행 하는 함수 기반으로 사용자가 정의한 일정에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Hello Azure 포털의에서 기능 앱 만들기](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="0df3d-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0df3d-106">Prerequisites</span></span>

<span data-ttu-id="0df3d-107">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="0df3d-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="0df3d-108">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="0df3d-109">Azure Function 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0df3d-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![함수 앱을 성공적으로 만들었습니다.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="0df3d-111">다음으로 hello 새 함수 앱에서 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="0df3d-112">타이머 트리거 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="0df3d-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="0df3d-113">함수에서 사용 하는 앱을 확장 하 고 hello 클릭  **+**  너무 단추 옆**함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="0df3d-114">Hello 함수 응용 프로그램에서 첫 번째 함수 이면 선택 **사용자 정의 함수**합니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="0df3d-115">이 함수 템플릿의 hello 전체 집합을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-115">This displays hello complete set of function templates.</span></span>

    ![Hello Azure 포털의에서 빠른 시작 페이지 함수](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="0df3d-117">선택 hello **TimerTrigger** 원하는 언어에 대 한 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="0df3d-118">다음 hello 테이블에 지정 된 hello 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-118">Then use hello settings as specified in hello table:</span></span>

    ![Hello Azure 포털에서에서 타이머 트리거 함수를 만듭니다.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="0df3d-120">설정</span><span class="sxs-lookup"><span data-stu-id="0df3d-120">Setting</span></span> | <span data-ttu-id="0df3d-121">제안 값</span><span class="sxs-lookup"><span data-stu-id="0df3d-121">Suggested value</span></span> | <span data-ttu-id="0df3d-122">설명</span><span class="sxs-lookup"><span data-stu-id="0df3d-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="0df3d-123">**함수 이름 지정**</span><span class="sxs-lookup"><span data-stu-id="0df3d-123">**Name your function**</span></span> | <span data-ttu-id="0df3d-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="0df3d-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="0df3d-125">타이머 트리거 함수의 hello 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="0df3d-126">**[일정](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="0df3d-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="0df3d-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="0df3d-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="0df3d-128">6 개의 필드 [CRON 식](http://en.wikipedia.org/wiki/Cron#CRON_expression) 함수 toorun를 예약 하는 1 분 마다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="0df3d-129">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-129">Click **Create**.</span></span> <span data-ttu-id="0df3d-130">함수는 1분마다 실행되는 선택한 언어로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="0df3d-131">Toohello 로그를 기록 하는 추적 정보를 확인 하 여 실행을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![뷰어 hello Azure 포털에에서 로그인 하는 함수입니다.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="0df3d-133">이제 같은 시간 마다 한 번씩, 자주 실행 되도록 hello 함수 일정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="0df3d-134">업데이트 hello 타이머 일정</span><span class="sxs-lookup"><span data-stu-id="0df3d-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="0df3d-135">함수를 확장하고 **통합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="0df3d-136">입력 정의 및 사용자가 함수에 대 한 바인딩 출력와 hello 일정을 설정할 수도 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="0df3d-137">`0 0 */1 * * *`의 새 **일정** 값을 입력한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![함수는 hello Azure 포털에서에서 일정 타이머를 업데이트합니다.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="0df3d-139">함수는 이제 한 시간마다 한 번씩 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="0df3d-140">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="0df3d-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="0df3d-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0df3d-141">Next steps</span></span>

<span data-ttu-id="0df3d-142">일정에 따라 실행되는 함수를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0df3d-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="0df3d-143">타이머 트리거에 대한 자세한 내용은 [Azure Functions를 사용하여 코드 실행 예약](functions-bindings-timer.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0df3d-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>