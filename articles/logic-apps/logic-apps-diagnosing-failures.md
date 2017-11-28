---
title: "오류 진단 - Azure Logic Apps | Microsoft Docs"
description: "Logic Apps이 실패하는 경우를 이해하는 일반적인 방법"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 814e6f93088cdd96b0a663d2a7494b5a11470d99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="93c31-103">논리 앱 오류 진단</span><span class="sxs-lookup"><span data-stu-id="93c31-103">Diagnose logic app failures</span></span>
<span data-ttu-id="93c31-104">Logic Apps에서 문제 또는 오류가 발생하는 경우 오류의 원인을 파악하는 데 도움이 되는 방법이 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="93c31-105">Azure 포털 도구</span><span class="sxs-lookup"><span data-stu-id="93c31-105">Azure portal tools</span></span>
<span data-ttu-id="93c31-106">Azure 포털에서는 각 단계에서 각 논리 앱을 진단하는 여러 가지 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="93c31-107">트리거 기록</span><span class="sxs-lookup"><span data-stu-id="93c31-107">Trigger history</span></span>

<span data-ttu-id="93c31-108">각 논리 앱에는 하나 이상의 트리거가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="93c31-109">앱이 실행되지 않는다는 점을 알아챈 경우 자세한 정보에 대한 트리거 기록을 먼저 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="93c31-110">트리거 기록은 논리 앱의 주 블레이드에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![트리거 기록 찾기][1]

<span data-ttu-id="93c31-112">트리거 기록은 만든 논리 앱의 모든 트리거 시도를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="93c31-113">각 트리거 시도를 클릭하여 세부 정보 특히, 트리거 시도로 생성된 모든 입력 또는 출력을 자세히 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="93c31-114">실패한 트리거를 찾는 경우 트리거 시도를 선택하고 **출력** 링크를 선택하여 유효하지 않은 FTP 자격 증명과 같은 생성된 오류 메시지를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="93c31-115">여러 상태가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="93c31-116">**생략**.</span><span class="sxs-lookup"><span data-stu-id="93c31-116">**Skipped**.</span></span> <span data-ttu-id="93c31-117">끝점을 폴링하여 데이터를 확인하고, 사용할 수 있는 데이터가 없다는 응답을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="93c31-118">**성공**.</span><span class="sxs-lookup"><span data-stu-id="93c31-118">**Succeeded**.</span></span> <span data-ttu-id="93c31-119">트리거가 데이터를 사용할 수 있다는 응답을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="93c31-120">이 상태는 수동 트리거, 되풀이 트리거 또는 폴링 트리거로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="93c31-121">이 상태는 일반적으로 **발생(Fired)** 상태와 함께 발생하지만 코드 보기에서 충족되지 않는 조건 또는 SplitOn 명령이 있는 경우에는 발생하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="93c31-122">**실패**.</span><span class="sxs-lookup"><span data-stu-id="93c31-122">**Failed**.</span></span> <span data-ttu-id="93c31-123">오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="93c31-124">트리거 수동 시작</span><span class="sxs-lookup"><span data-stu-id="93c31-124">Start a trigger manually</span></span>

<span data-ttu-id="93c31-125">논리 앱에서 사용 가능한 트리거를 즉시(다음 되풀이까지 기다리지 않고) 확인하려면 주 블레이드에서 **트리거 선택** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="93c31-126">예를 들어 Dropbox 트리거로 이 단추를 클릭하면 새 파일에 대해 Dropbox를 즉시 폴링하는 워크플로가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="93c31-127">실행 기록</span><span class="sxs-lookup"><span data-stu-id="93c31-127">Run history</span></span>

<span data-ttu-id="93c31-128">발생한 트리거는 모두 실행 중에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="93c31-129">주 블레이드에서 실행 정보에 액세스할 수 있습니다. 여기에는 워크플로에서 일어난 일을 이해할 수 있는 세부 정보가 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![실행 기록 찾기][2]

<span data-ttu-id="93c31-131">실행은 다음 상태 중 하나를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="93c31-132">**성공**.</span><span class="sxs-lookup"><span data-stu-id="93c31-132">**Succeeded**.</span></span> <span data-ttu-id="93c31-133">모든 작업에 성공했습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-133">All actions succeeded.</span></span> <span data-ttu-id="93c31-134">오류가 발생한 경우 나중에 워크플로에서 발생한 작업으로 처리되었습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="93c31-135">즉, 작업이 실패하고 실행되도록 설정된 작업에서 오류를 처리했습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="93c31-136">**실패**.</span><span class="sxs-lookup"><span data-stu-id="93c31-136">**Failed**.</span></span> <span data-ttu-id="93c31-137">하나 이상의 작업이 실패하였고, 그중 워크플로에서 나중에 발생하여 처리하지 못한 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="93c31-138">**취소**.</span><span class="sxs-lookup"><span data-stu-id="93c31-138">**Cancelled**.</span></span> <span data-ttu-id="93c31-139">워크플로가 실행 중이지만 취소 요청을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="93c31-140">**실행 중**.</span><span class="sxs-lookup"><span data-stu-id="93c31-140">**Running**.</span></span> <span data-ttu-id="93c31-141">워크플로가 현재 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-141">The workflow is currently running.</span></span> <span data-ttu-id="93c31-142">이 상태는 제한되는 워크플로 또는 현재 요금제로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="93c31-143">자세한 내용은 [가격 책정 페이지의 작업 제한](https://azure.microsoft.com/pricing/details/app-service/plans/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93c31-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="93c31-144">진단 구성(실행 기록 아래에 나타나는 차트)은 발생한 제한 이벤트에 관한 정보를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="93c31-145">실행 기록에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="93c31-146">트리거 출력</span><span class="sxs-lookup"><span data-stu-id="93c31-146">Trigger outputs</span></span>

<span data-ttu-id="93c31-147">트리거 출력은 트리거에서 온 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="93c31-148">이러한 출력은 모든 속성이 예상대로 반환되었는지 확인하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="93c31-149">이해할 수 없는 콘텐츠가 있는 경우 Azure Logic Apps에서 [다양한 콘텐츠 유형을 처리](../logic-apps/logic-apps-content-type.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![트리거 출력 예제][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="93c31-151">작업 입력 및 출력</span><span class="sxs-lookup"><span data-stu-id="93c31-151">Action inputs and outputs</span></span>

<span data-ttu-id="93c31-152">작업에서 수신한 입력 및 출력을 드릴인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="93c31-153">이 데이터는 출력 크기와 셰이프를 이해하고 생성될 수 있는 오류 메시지를 찾는 데에도 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![작업 입력 및 출력][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="93c31-155">워크플로 런타임 디버그</span><span class="sxs-lookup"><span data-stu-id="93c31-155">Debug workflow runtime</span></span>

<span data-ttu-id="93c31-156">입력, 출력 및 실행 트리거를 모니터링하는 것 외에도 워크플로에 디버깅에 도움이 되는 몇 가지 단계를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="93c31-157">[RequestBin](http://requestb.in) 이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="93c31-158">RequestBin을 사용하면 HTTP 요청의 크기, 모양 및 형식을 정확하게 파악하도록 HTTP 검사기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="93c31-159">RequestBin을 만들고 URL을 테스트하려는 본문 콘텐츠(예: 식, 다른 단계 출력)와 논리 앱 HTTP POST 작업에 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="93c31-160">논리 앱을 실행한 후에는 RequestBin을 새로 고쳐 Logic Apps 엔진에서 생성되는 경우 요청이 어떻게 형성되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93c31-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
